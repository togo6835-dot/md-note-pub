# 指数関数 $\exp$ の数値計算は不安定...

## 1. 何が問題なのか

数値計算では、指数関数

```math
\exp(x)
```

が非常に急激に増減するため、変数 $x$ が大きすぎたり小さすぎたりすると、計算機で正しく扱えなくなる。

### overflow

大きすぎて表現できない状態を**overflow**と呼ぶ。たとえば倍精度では、おおよそ

```math
x \gtrsim 709.78
```

で

```math
\exp(x)
```

は有限値として表現できず、`inf` になりうる。

### underflow

小さすぎて表現できない状態を**underflow**と呼ぶ。たとえば

```math
\exp(-1000)
```

のような値は、実際には極小の正数だが、計算機では$0$として扱われることがある。

### NaN

overflow や underflow の結果として、

```math
\frac{\infty}{\infty},\qquad \frac{0}{0},\qquad \infty-\infty
```

のような不定形が現れると、`NaN` が発生する。

>つまり、
>
>$$
>\frac{\exp(1000)+\exp(1001)}{\exp(999)}
>$$
>
>のような計算を素朴に行うと非常に危険。
>ちなみに、[TensorFlow](https://www.tensorflow.org/api_docs/python/tf/nn/sigmoid_cross_entropy_with_logits)や[Pytorch](https://docs.pytorch.org/docs/stable/generated/torch.nn.functional.log_softmax.html?utm_source=chatgpt.com)ではデフォルトで対策がなされている（以下で説明する方法）。
---


## 2. 基本方針

本質は一つである。

```math
\text{大きい } \exp \text{ を直接作らない}
```

そのために、次のような工夫を行う。

1. 対数のまま持つ  
2. 最大値や最小値を引く  
3. 和は log-sum-exp を使う  
4. 比は差で計算する  
5. 必要なら場合分けして指数の中身を非正にする  

---

## 3. 最大値を引く方法

たとえば

```math
w_i = \exp(a_i)
```

という重みがあるとする。  
これをそのまま計算すると、`a_i` が大きいと overflow する。

そこで

```math
m = \max_i a_i
```

を取って

```math
w_i = \exp(a_i-m)\exp(m)
```

と書く。  
正規化にしか使わないなら共通因子 `exp(m)` は消えるので、

```math
\tilde w_i = \exp(a_i-m)
```

だけを計算すればよい。

このとき

```math
a_i-m \le 0
```

なので、指数の中身は常に非正となり、安全になる。

---

## 4. softmax の安定化

softmax は

```math
p_i = \frac{\exp(a_i)}{\sum_j \exp(a_j)}
```

で定義されるが、これは素朴に計算してはいけない。

安定な形は

```math
m=\max_j a_j
```

として

```math
p_i=\frac{\exp(a_i-m)}{\sum_j \exp(a_j-m)}
```

である。

これにより、分子・分母に現れる指数の中身がすべて非正になる。

---

## 5. log-sum-exp trick

和

```math
\sum_i \exp(a_i)
```

そのものを計算するのも危険である。  
このときは

```math
\mathrm{LSE}(a_1,\dots,a_N)=
\log\left(\sum_{i=1}^N \exp(a_i)\right)
```

を直接ではなく、

```math
m=\max_i a_i
```

を用いて

```math
\log\left(\sum_i \exp(a_i)\right)=
m+\log\left(\sum_i \exp(a_i-m)\right)
```

と計算する。

これが **log-sum-exp trick** である。

### なぜ安全か

すべての `a_i-m` は非正なので、

```math
\exp(a_i-m)\le 1
```

であり、巨大な指数が出ない。

---

## 6. 確率の正規化との関係

log probability

```math
x_i = \log p_i
```

が与えられたとき、正規化された確率は

```math
p_i = \frac{\exp(x_i)}{\sum_n \exp(x_n)}
```

である。

これを安全に計算するには

```math
\log p_i=
x_i-\log\left(\sum_n \exp(x_n)\right)
```

とし、さらに log-sum-exp を用いて

```math
\log\left(\sum_n \exp(x_n)\right)=
m+\log\left(\sum_n \exp(x_n-m)\right),
\qquad m=\max_n x_n
```

と計算する。

---

## 7. `e^{-S}` 型の重みに対する適用

論文や統計力学、経路積分では

```math
w_i = e^{-S_i}
```

のような重みが現れる。  
ここで `S_i` が大きくばらつくと、やはり数値的に不安定になる。

このときは

```math
S_{\min} = \min_i S_i
```

を取って

```math
w_i = e^{-(S_i-S_{\min})}e^{-S_{\min}}
```

と書く。  
正規化だけが必要なら共通因子 `e^{-S_{\min}}` は不要なので、

```math
\tilde w_i = e^{-(S_i-S_{\min})}
```

だけ計算すればよい。

ここでは

```math
S_i-S_{\min}\ge 0
```

だから

```math
-(S_i-S_{\min})\le 0
```

であり、指数の中身が非正になる。

### 正規化重み

```math
p_i=
\frac{e^{-S_i}}{\sum_j e^{-S_j}}=
\frac{e^{-(S_i-S_{\min})}}{\sum_j e^{-(S_j-S_{\min})}}
```

### 分配関数の対数

```math
\log\left(\sum_i e^{-S_i}\right)=
-S_{\min}
+
\log\left(\sum_i e^{-(S_i-S_{\min})}\right)
```

これは

```math
x_i=-S_i
```

とおいた log-sum-exp trick そのものである。

---

## 8. 差だけ必要なら差で計算する

比

```math
\frac{e^a}{e^b}
```

は、それぞれを別に指数化するより

```math
e^{a-b}
```

と書く方が安全である。

同様に

```math
\frac{e^{-S(\phi)}}{e^{-S(\chi)}} = e^{-(S(\phi)-S(\chi))}
```

である。  
絶対値ではなく差が本質なら、最初から差で計算する。

---

## 9. Metropolis 型の受理率

たとえば

```math
A=\min\{1,e^{-\Delta S}\}
```

を計算する場合、素朴に常に指数を計算する必要はない。  
次のように分岐すればよい。

```math
\Delta S \le 0 \Rightarrow A=1
```

```math
\Delta S > 0 \Rightarrow A=e^{-\Delta S}
```

これなら、実際に計算する指数の中身は常に非正である。

---

## 10. 深層学習でも同じことをしている

深層学習ライブラリでも、この種の数値安定化は標準である。

### softmax / log-softmax

```math
\log(\mathrm{softmax}(x))
```

を素朴に

```math
\log\left(\frac{e^{x_i}}{\sum_j e^{x_j}}\right)
```

と計算すると不安定なので、内部では最大値を引いた形や log-sum-exp が使われる。

### cross entropy

softmax を明示的に計算してから log を取るのではなく、logits から直接、安定な形で loss を計算する。

### sigmoid cross entropy

2値分類の損失では

```math
x-xz+\log(1+\exp(-x))
```

のような式が現れるが、`x<0` で `exp(-x)` が危険になる。  
そこで

```math
\max(x,0)-xz+\log(1+\exp(-|x|))
```

のように、指数の中身が非正になる等価変形を用いる。

---

## 11. TensorFlow の `sigmoid_cross_entropy_with_logits` の意味

`sigmoid_cross_entropy_with_logits` では、損失が最終的に

```math
x-xz+\log(1+\exp(-x))
```

と書ける。  
しかし `x<0` だと `-x>0` なので、`exp(-x)` が大きくなり危険である。

そこで実装では

```math
\max(x,0)-xz+\log(1+\exp(-|x|))
```

を使う。

ここで

```math
-|x|\le 0
```

なので、指数関数は安全である。

---

## 12. PyTorch でも同様

PyTorch でも

- `log_softmax`
- `cross_entropy`
- `BCEWithLogitsLoss`

などが、内部で安定化された形を用いる。

つまり、

```math
\exp
```

をむき出しで計算するより、

- `log_softmax`
- `logsumexp`
- `cross_entropy`
- `binary_cross_entropy_with_logits`

のような関数を使うのが基本である。

---

## 13. 直感的な理解

本質は、数式の上では有限でも、計算機では途中計算が壊れるという点にある。

たとえば

```math
\frac{\exp(1000)}{\exp(1000)+\exp(999)}
```

は数学的には有限だが、計算機はまず `exp(1000)` を表現できない。  
そこで

```math
\frac{\exp(0)}{\exp(0)+\exp(-1)}
```

のように同値変形してから計算する必要がある。

---

## 14. 実務的な指針

指数関数が現れたら、次を確認するとよい。

### 和の中に `exp` がある

```math
\sum_i \exp(a_i)
```

なら log-sum-exp を使う。

### 正規化重み

```math
\frac{\exp(a_i)}{\sum_j \exp(a_j)}
```

なら最大値を引く。

### `e^{-S}` 型

```math
e^{-S_i}
```

なら `S_{\min}` を引いて

```math
e^{-(S_i-S_{\min})}
```

にする。

### 比

```math
\frac{e^a}{e^b}
```

なら

```math
e^{a-b}
```

にする。

### 受理率

```math
\min\{1,e^{-\Delta S}\}
```

なら符号で分岐する。

### できれば log のまま保持

確率や重みは、可能なら

```math
p
```

ではなく

```math
\log p
```

を保持する。

---

## 16. 結論

指数関数が入る数値計算では、次が中心原理である。

```math
\text{大きい指数を直接作らない}
```

そのための代表的手法は

1. 最大値・最小値を引く  
2. log-sum-exp を使う  
3. 差で計算する  
4. log のまま持つ  
5. 必要に応じて安定な等価変形を使う  

である。

特に

```math
e^{-S}
```

型の重みでは

```math
e^{-S_i}
\quad\longrightarrow\quad
e^{-(S_i-S_{\min})}
```

という変形が基本であり、これは深層学習で使われる softmax や BCE の数値安定化と本質的に同じ発想である。