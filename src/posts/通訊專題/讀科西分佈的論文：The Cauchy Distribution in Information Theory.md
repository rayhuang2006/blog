# The Cauchy Distribution in Information Theory

>[!info]
這篇文最重要的就是讀這篇論文：[The Cauchy Distribution in Information Theory](https://www.mdpi.com/1099-4300/25/2/346)，我就照著我的理解把所有東西全部打一次，但看起來大概會很囉唆，因為我是一邊讀一邊打得，算是一個講稿這樣，當然也可以想像成他是一個超級人性化的翻譯。


## Section 1 Introduction
首先最開篇的時候，作者說現在高斯分佈已經是連續隨機變數的最重要的例子，為什麼呢？作者講了很多，首先作者說他的 information measures （我的理解是這是一個測量訊號裡的資訊有多少、多亂、多相似的一個數值）可以寫成closed-form expressions（應該就是可以寫成一個比較漂亮的數學式子，就是說可以不需要用那些數值方法去求他這樣）

然後他講了一下高斯分佈可以利用在一些例子上（比如說，類比資訊源（analog information sources）或者是加成性熱雜訊（additive thermal noise）這些我都沒有很確定是什麼意思，但我想這個大概可能也不太會是這篇的重點，可能只是個引言，所以我就沒有特別去查是什麼意思），甚至是很重要的地位，他的意思就是說，這個東西在現在很重要這樣。

然後，對然後，這裡是第一個小轉折，他要開始講一些不一樣的，他第一個提及的是指數分佈，他的意思就是說哎呀，指數分佈也不錯啊，指數分佈也在很多情況下也可以寫成一個closed-form expressions，比如說：微分熵 differential entropy、互資訊 mutual information、相對熵 relative entropy之類的或者說一些具有記憶性的連續時間模型（例如指數伺服器佇列 exponential-server queue）中，它也能算出率失真函數和通道容量 。

好講完指數分佈之後，他終於進入他想講的重點，他開始推銷他的Cauchy distribution，他說哎呀雖然這個Cauchy有一個最經典的問題就是他 lack of moments，怎麼理解呢？也就是說他沒辦法求出常規的mean 以及 variance，但是，但是呢，作者發現這個 Cauchy distribution 的某些 imformation measures 竟然也能寫成 closed-form expressions。

除了這件事情之外呢，他又說，哎呀雖然我們前面提到了他lack of moments，但他引入了一個新的東西叫做「strength」，用來分析他的「胖瘦」（就像 Var 的角色對於 Gaussian 來說是一樣的），然後在這個全新的體系下，他會是「最優的」（也就是文中說的 possess optimality properties，就像在 Var 中，Gaussian 也是最優的一樣）

最後作者總結說，他後面會清楚的講，根據Cauchy 的stability（穩定性，也就是說，兩個科西分佈加起來也會是科西分佈），他可以推導出了對應高斯經典基本極限（如通道容量、率失真函數）的柯西版本。

>[!note]- 原本之前在Gausian的通道容量，率失真函數那些
>- 通道容量：
>   $$C = \frac{1}{2} \log(1 + \text{SNR})$$，其中 SNR（訊噪比）就是訊號變異數除以雜訊變異數（$\frac{\sigma_X^2}{\sigma_N^2}$）。描述在有雜訊的通道中，能夠無失真傳輸資料的「最高速率」（我的理解就是這個東西就是說在一條有雜訊的高速公路上，車子的最高速限可以跑多快而且不會發生車禍，是一個理論極限這樣）。
>- 率失真函數：
 >   $$R(D) = \frac{1}{2} \log(\frac{\sigma^2}{D})$$
 >    描述在允許一定程度的「失真（Distortion, 通常用均方誤差 MSE，也就是變異數來衡量）下，資料可以被壓縮到的「最低傳輸速率」。（首先這就是把現實世界的問題數學化，當想要高清影片（變異低）的時候，檔案就會很大，當對影片畫質要求沒那麼高的時候，檔案就可以壓縮的很小）


## Section 2 The Cauchy Distribution and Generalizations

在最一開始，作者先引用了最經典的最經典的 Cauchy 密度函數：

$$f_V(x) = \frac{1}{\pi(x^2 + 1)}, \quad x \in \mathbb{R} \quad$$

這就是 Cauchy 最原本的樣子，大概也是沒有特別好解釋的，文中他是用 $V$去表示，把標準的 $V$ 乘上一個倍數 $\lambda$，再加上一個平移值 $\mu$，也就是說$X = \lambda V + \mu$，帶進去公式裡面就會看到第二條式子：

$$f_X(x) = \frac{1}{\pi} \frac{|\lambda|}{(x-\mu)^2 + \lambda^2}, \quad x \in \mathbb{R} \quad$$

這就是一般化 Cauchy 分佈公式，$\mu$ 在文中他說叫做 location 或者說叫做 median，我們也可以很清楚的看得出來，這個東西就是一個偏移量，決定他的中心在哪裡，如果 $\mu = 0$ 沒有發生偏移，我們就叫他 centered Cauchy 。然後在 $|\lambda|$ 叫做 scale ，也蠻直觀的，他會決定這個東西到底有多胖多瘦，這些也可以對應到 introduction 中他說過的 Cauchy 沒有 Variance 以及 Mean，所以他用了這兩個東西去替代，來去衡量 Cauchy 的位置跟胖瘦。

雖然前面一直強調說沒有 Cauchy 沒有 Mean 跟 Variance，但似乎沒有詳細說明過，所以作者接下來詳細的解釋一下為什麼 Cauchy 沒有這些東西，首先雖然從帶入期望值的公式來看，這個式子：$$\int_{-\infty}^{\infty} x \cdot f_V(x) dx$$ 好像是對稱於 0 ，但是如果仔細分開來檢查，分別定義

$$V^+ = \max\{0, V\}$$

$$V^- = \max\{0, -V\}$$

那麼我們就可以拆分整個期望值變成

 $$\mathbb{E}[V] = \mathbb{E}[V^+] - \mathbb{E}[V^-]$$   

然後我們就會如同文中一樣發現一個驚人的事實：

$$\mathbb{E}[\max\{0,V\}] = \mathbb{E}[\max\{0,-V\}] = \infty$$，那麼這個期望值就會變成 $\infty - \infty$，變成未定，當然就更不要說 $\mathbb{E}[|V|^q]$ 在 $q \ge 1$ 的情況下了，整個動差母函數都是爆炸的。

>[!note]- 測度論與勒貝格積分
我其實有稍微有印象中之前彥奇老師的機率論有講過，但是我翻我的筆記跟記憶不是很確定，所以我有稍微翻一下網路上的資料，做一些整理這樣：
>
課堂上有講過，整個機率論是建築在一個測度空間 $(\Omega, \mathcal{F}, \mathbb{P})$ 之上的，當然測度有很多定義，這裡我就沒有一一敘述。但是在這個嚴格的體系之下，我們求所謂的期望值 $\mathbb{E}[X]$ 本質上就是在這個機率空間上做勒貝格積分（Lebesgue Integral），也就是 $$\mathbb{E}[X] = \int X \, d\mathbb{P}$$ ，而勒貝格積分有個嚴格的規定就是一個函數要是可積，那麼就要滿足 $\int X^+ < \infty$ 而且  $\int X^- < \infty$ 這也就是為什麼論文中簡單敘述之後就判定這個期望值不存在。
>
但為什麼一定要這麼做呢，我的理解是如果只是讓他條件收斂，那麼根據分析導論中提到過的 Riemann Rearrangement Theorem ：一個無窮級數只有「條件收斂」（像柯西主值那樣強制對稱相加），只要刻意改變它相加的順序，總和可以變成任何實數。
>
期望值的本質是「大量隨機樣本的平均」。在現實中，抽到極端正數和極端負數的「順序」是完全隨機的。如果期望值只有條件收斂，這意味著「因為抽樣順序（運氣）的不同，算出來的長期平均值可能會是 0，也可能會跑到 100 萬，或變成負無窮大」。一個會因為抽樣順序不同而得出完全不同結果的期望值，在物理和統計上是毫無意義的。這就是為什麼作者必須嚴謹地宣告 $\infty - \infty$，代表 Cauchy 在機率論的嚴格標準下，期望值絕對不存在。

既然動差母函數是爆炸的，那我們應該怎麼去分析這個東西呢？誒，作者引入了另一個機率論的概念，叫做「特徵函數 (Characteristic Function)」，他的想法很簡單，就是把原本的動差母函數補上虛數 $i$ ，這樣寫成積分形式就會變成：
$$\int_{-\infty}^{\infty} f_V(x) e^{i\omega x} dx$$

根據尤拉公式，我們會發現他最終會變成由 $sin$, $cos$ 之類的組成，而這兩個函數絕對值永遠以 $1$ 為界（$|e^{i\omega x}| = 1$））怎麼樣都會收斂。

太棒了，然後作者幫我們做了一下中間的微積分計算，得到科西的特徵函數$$\mathbb{E}[e^{i\omega V}] = e^{-|\omega|}$$

有了這個特徵函數之後，我們就會發現一些很有趣的事情，首先如果有兩個獨立的標準科西變數 $V_1$ 和 $V_2$，我們把它們加起來，特徵函數會變怎樣？

$$\mathbb{E}[e^{i\omega (V_1 + V_2)}] = \mathbb{E}[e^{i\omega V_1}] \times \mathbb{E}[e^{i\omega V_2}] = e^{-|\omega|} \times e^{-|\omega|} = e^{-2|\omega|}$$

那如果如果是直接把一個科西變數放大兩倍（$2V$）呢？

$$\mathbb{E}[e^{i\omega (2V)}] = e^{-|2\omega|} = e^{-2|\omega|}$$

這時候我們發現一件很有趣的事情，在統計上，我們加上一個，加上一個獨立的 Cauchy 變數，等同於直接加上一個一模一樣的副本 。這使得 Cauchy 分佈與高斯分佈一樣，具備了「穩定性 (Stable)」。也就是說，多個 Cauchy 變數做線性組合後，依然會是 Cauchy 分佈 。

這會導致什麼呢？平常很好用的的「時間平均 (Time average)」再也無法消除雜訊了，作者在文中指出，如果我們對 $n$ 個獨立且同分佈的 Cauchy 隨機變數取平均（$\frac{1}{n}\sum_{i=1}^n V_i$），它最終的分佈會與任何單一一個 Cauchy 變數的分佈完全相同 。這意味著，無論你收集多少數據來取平均，都無法讓變異收斂（因為它根本沒有變異數），傳統的大數法則在這裡徹底崩潰。

然後作者補充了一些 Cauchy 的經典性質，首先，如果 $\Theta \sim U[-\frac{\pi}{2}, \frac{\pi}{2}]$那麼 $V = \tan(\Theta)$ 是標準的 Cauchy 分佈。然後作者通過一些數學推論，給出了 Cauchy 的標準 CDF：
$$F_V(x) = \frac{1}{2} + \frac{1}{\pi}\arctan(x), \quad x \in \mathbb{R}$$
以及 Cauchy 的分位數函數 (Quantile function)：
$$Q_V(t) = \tan\left(\pi\left(t - \frac{1}{2}\right)\right), \quad t \in (0,1)$$
也就是 CDF 的反函數，由此我們也可以看出，標準 Cauchy 具有「單位的半四分位距 (unit semi-interquartile length)」


>[!note]- 也就是說
$$Q_3 = Q_V(0.75) = tan(\pi * 0.25) = tan(\frac{\pi}{4}) = 1$$$$Q_1 = Q_V(0.25) = tan(-\frac{\pi}{4}) = -1$$$$ \frac{Q_3 - Q_1}{2} = 1$$

如果 $X_1$ 和 $X_2$ 是兩個標準高斯分佈，而且他們具有相關係數$\rho \in (-1, 1)$，那麼將它們相除 ($X_1/X_2$) 那麼就會產生一個 Scale 為 $\sqrt{1-\rho^2}$ 以及 location 為 $\rho$ 的一般化科西分佈。

也就是說，如果$\rho=0$，那麼 $\frac{X_1}{X_2}$ 就是標準的 Cauchy 分佈，這也就意味著，標準 Cauchy 的倒數 $\frac{1}{V}$ 依然是 Cauchy。

這一切到目前為止都蠻順的，但是當到推展到 n 維時，開始出現了一些問題，在數學上，一個隨機向量被稱為「多變數 Cauchy」，其充分必要條件是：「它任何分量的線性組合，都必須服從 Cauchy 分佈」。

但問題在於：目前數學界還無法寫出這種一般化多變數 Cauchy 的通用機率密度函數 (PDF)！

所以這篇論文會依賴一個已知且漂亮的特例，就是這個Standard spherical multivariate Cauchy，他在$\mathbb{R}^n$下會長這樣：

$$f_{V^n}(x) = \frac{\Gamma(\frac{n+1}{2})}{\pi^{\frac{n+1}{2}}}(1+||x||^2)^{-\frac{n+1}{2}}$$

他有幾個比較漂亮的性質，首先延續一維的高斯相除概念，如果我們有 $n+1$ 個獨立的標準高斯變數 $X_0, X_1, \dots, X_n$，那麼只要將向量 $X^n$ 統統除以 $X_0$（也就是 $X_0^{-1}X^n$），就會得到這個標準球面 Cauchy 分佈。

其次是他是 Marginal 的，也就是說，它的任何一個子集合、任何單一分量，都依然服從標準 Cauchy 分佈。

然後他的特徵函數一樣是漂亮的：

$$\mathbb{E}[e^{i \mathbf{t}^\top \mathbf{V}^n}] = e^{-||\mathbf{t}||}$$

變成了向量長度的負指數。

之後為了讓整個公式更加的通用，透過 Affline transformation $\mathbf{Z}^n = \Lambda^{\frac{1}{2}} \mathbf{V}^n + \mu$ 把這個球面 Cauchy 拉伸並平移成橢圓形 Cauchy：

$$f_{\mathbf{Z}^n}(\mathbf{z}) = \frac{\Gamma(\frac{n+1}{2})}{\pi^{\frac{n+1}{2}} |\Lambda|^{\frac{1}{2}}} \left( 1 + (\mathbf{z} - \mu)^\top \Lambda^{-1} (\mathbf{z} - \mu) \right)^{-\frac{n+1}{2}}$$

>[!note]- 簡單推導
就如果我們要做這個變換：$$Z = \Lambda^{1/2} V + \mu$$，
我們就把 $V$ 反解出來帶入原本的公式：
$$V = \Lambda^{-1/2} (Z - \mu)$$
公式裡面原本還有$||V||^2$，一起推論：
$$||V||^2 = V^\top V = (Z - \mu)^\top (\Lambda^{-1/2})^\top (\Lambda^{-1/2}) (Z - \mu)$$
因為 $\Lambda$ 是對稱的正定矩陣，這串乘起來剛好就是：
$$||V||^2 = (Z - \mu)^\top \Lambda^{-1} (Z - \mu)$$
因為我們用矩陣 $\Lambda^{1/2}$ 把空間拉伸了，機率的「體積」會改變。根據微積分的變數代換公式，PDF 必須乘上一個 Jacobian 係數，也就是反函數行列式的絕對值：
$$|\det(\Lambda^{-1/2})| = |\det(\Lambda)|^{-1/2}$$
把這些推倒全部帶進去，就會得到那條公式了。

當這個模型作者也有提到有兩個很大的問題：
- 第一是它無法涵蓋所有多變數的情況，特別是無法描述「各分量彼此獨立的 Cauchy 變數」。
- 第二是說他 not closed under independent additions ，也就是說兩個獨立的橢圓 Cauchy 向量相加後，其 PDF 通常無法再用原本的公式來表示。

最後作者提到了 Cauchy 的寫法，引入 1958 由 Rider 設計的公式：

$$f_{V_{\beta,\rho}}(x) = \frac{\kappa_{\beta,\rho}}{(1+|x|^\rho)^\beta}$$

其中：$$\kappa_{\beta, \rho} = \frac{\rho \Gamma(\beta)}{2 \Gamma(1/\rho) \Gamma(\beta - 1/\rho)}$$

當 $(\beta, \rho) = (1, 2)$ 他就是 Cauchy，當然，這個公式不只包含著 Cauchy ，調整參數$\rho=2$，$\beta=\frac{\nu+1}{2}$，然後再把 x 軸縮放 $\sqrt{\nu}$ 倍，它就會變成標準的 Student-t 分佈，也等價於說 Pearson Type VII 分佈（我查了一下，我的理解就是說這些就是那些同樣具有 heavy tail 性質的分佈）。

## Section3
































