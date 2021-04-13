---
title:  "고유값, 고유벡터"
last_modified_at: 2021-02-10T19:00:58-04:00
categories: 
  - Recommendation-Systems
tags:
  - Eigen_Value, Eigen_Vector
use_math: true
toc: true
toc_label: "Getting Started"
---

[추천시스템](https://github.com/jlim0316/Recommendation-Systems)을 공부하며 내용을 정리해보고자 한다. 

## Step 1: 기본 개념

`스칼라`, `벡터`, `행렬`이라는 기본 용어를 정리하면 다음과 같다.:

- Scalar: 숫자로서 크기만 갖는 물리량이다.
- Vector: 크기와 방향을 갖는 물리량으로, 좌표공간 내에서 시작점과 끝점을 연결할 수 있는 화살표이다.
- Matrix: 1개 이상의 벡터를 행과 열로서 배열해서 괄호로 묶어 놓은 형태이다.
{: .notice}

---
`고유값`, `고유벡터`의 기본 개념은 다음과 같다.:
- Eigen value: n차 정사각형행렬 A가 있다. 0이 아닌 벡터 $\chi\in\mathbb{R^{\textrm{n}}}$가 어떤 $\lambda$에 대하여 $A\lambda=\lambda X$를 만족하는 **$\lambda$**를 A의 `고유값(eigenvalue)`이라 한다.
- Eigen vector: 위 언급된 **$X$**를 $\lambda$에 대한 $A$의 `고유벡터(eigenvector)`라고 한다.
{: .notice}

---
`고유값 분해`의 기본 개념은 다음과 같다.:\\
행렬 $A$의 고유값 $\lambda_{i}$, 고유벡터 $v_{i}$라 하자. $1, 2,\ldots, n$. 그러면, `행렬 A에 대한 고유값 분해`는 아래와 같다.

 $$\begin{align*}
 A[v_{1}\,v_{2}\ldots\,v_{n}] & =  [\lambda_{1}v_{1}\,\lambda_{2}v_{2}\ldots\,\lambda_{n}v_{n}]\\
 & =  [v_{1}\,v_{2}\ldots\,v_{n}]{\begin{bmatrix}
\lambda_{1} & \cdots & 0\\
\vdots & \ddots & \vdots\\
0 & \cdots & \lambda_{n}\\
\end{bmatrix}}
\end{align*}$$
{: .notice}


## Step 2: 직관적인 이해
### Step 2-1: 방향 불변성
고유벡터와 행렬을 곱하면 크기는 늘어나거나 축소할 지언정 **방향은 바뀌지 않는다**. 
이는 위키피디아에서 확인 가능하다. 위키피디아에서 정의해둔 그림과 내용은 다음과 같다.<br>
<br>![image](https://user-images.githubusercontent.com/41845290/107492735-20a53680-6bd0-11eb-9461-bb7314cb6a0e.png)

Matrix A acts by stretching the vector x, not changing its direction, so x is an eigenvector of A. 
{: .notice}

---
고유값과 고유벡터에 관한 간단한 예를 통해 알아보자.<br>
<br>예를 들어 2차 정사각형 행렬 A가 다음과 같이 있다고 가정하자.
 
$$\begin{align*}
A&=&\begin{bmatrix}3 & 0\\
8 & 1\\
\end{bmatrix}\end{align*}$$
{: .notice}

특성방정식을 이용하여 고유값과 고유벡터를 계산하면<br> 고유값 $\lambda = 3, \;1$, 고유벡터는 $v_{1}=(0,1)$, $v_{2}=(1,4)$임을 계산할 수 있다.
 이는 [WolframAlpha](https://www.wolframalpha.com/input/?i=eigen+vectors+of+a+matrix&assumption=%7B%22F%22%2C+%22MatrixOperations%22%2C+%22theMatrix%22%7D+-%3E%22%7B%7B3%2C0%7D%2C%7B8%2C1%7D%7D%22&assumption=%7B%22MC%22%2C+%22%22%7D+-%3E+%7B%22Calculator%22%7D)에서도 고유값, 고유벡터 계산하는 것으로서 확인할 수 있다.


즉, 고유값 $\lambda$의 크기에 따라 고유 벡터는 확대, 축소라는 Streching만 하고 방향을 바꾸는 것은 아니다. 

---
예시 행렬이 $A\lambda=\lambda X$를 만족하는지 확인해보자.<br><br>$v_{1}=(0,1)$는 고유값 $\lambda_{1}=1$에 대응하는 2차 정사각형 행렬 $A$의 고유벡터이다. 


그 이유는 $$ \begin{align*}AX &= \begin{bmatrix}3 & 0\\
8 & 1\\
\end{bmatrix}\times\begin{bmatrix}\begin{array}{c}
0\\
1
\end{array}\end{bmatrix}\\&=\begin{bmatrix}\begin{array}{c}
0\\
1
\end{array}\end{bmatrix}\\&=1X\end{align*}$$ 이기 때문이다.
{: .notice}

또한, $v_{2}=(1,4)$는 고유값 $\lambda_{2}=3$에 대응하는 2차 정사각형 행렬 $A$의 고유벡터이다. 

그 이유는 $$ \begin{align*}AX &= \begin{bmatrix}3 & 0\\
8 & 1\\
\end{bmatrix}\times\begin{bmatrix}\begin{array}{c}
1\\
4
\end{array}\end{bmatrix}\\&=\begin{bmatrix}\begin{array}{c}
3\\
12
\end{array}\end{bmatrix}\\&=3X\end{align*}$$ 이기 때문이다.
{: .notice}
<br>
위키피디아에서 쓰여진 그림을 다시 가져와서 해당 예시 행렬로 고려해보면 다음과 같다. 행렬의 고유벡터에 행렬을 곱하면 크기만 변하고 방향은 변하지 않음을 확인할 수 있다.
<br>![image](https://user-images.githubusercontent.com/41845290/107492855-3d416e80-6bd0-11eb-9d71-8b57fe182794.png)




---
### Step 2-2: 고유값과 고유벡터 구하는 법
고유값과 고유벡터를 구하는 자세한 방법은 아래와 같다.
특성방정식을 통해 <br>**고유값**부터 구해보면 다음과 같다.

$$\begin{align*}
|A-\lambda I|=\left|\begin{array}{cc}
3-\lambda & 0\\
8 & 1-\lambda
\end{array}\right|=0\\\Leftrightarrow(3-\lambda)(1-\lambda)=0\\\Rightarrow \lambda^{2}-4\lambda+3=0\\\therefore\lambda=1,3
\end{align*}$$
{: .notice}
<br>
이제 고유값을 이용해 **고유벡터**를 구해보자. $\lambda=1$일때,

$$\begin{align*}
(A-\lambda I)\times X &=(A-1I)\times X\\&=\begin{bmatrix}\begin{array}{cc}
3-1 & 0\\
8 & 1-1
\end{array}\end{bmatrix}\times\begin{bmatrix}\begin{array}{c}
a\\
b
\end{array}\end{bmatrix}=0\\&=\begin{bmatrix}\begin{array}{cc}
2 & 0\\
8 & 0
\end{array}\end{bmatrix}\times\begin{bmatrix}\begin{array}{c}
a\\
b
\end{array}\end{bmatrix}=0\\
\\\Rightarrow 2a &= 0 \Leftrightarrow a = 0 \\\therefore a = 0
\\
\\a=0일때 \; 0\times b =0이므로 \; b는 \; 임의의 \; 값이 \; 올 \;수 \;있다.\\
여기서 \; 임의의 \; 값을 \; 1이라 \; 두겠다.
\\\Rightarrow X &= \begin{bmatrix}\begin{array}{c}
a\\
b
\end{array}\end{bmatrix}= \begin{bmatrix}\begin{array}{c}
0\\
b
\end{array}\end{bmatrix}= \begin{bmatrix}\begin{array}{c}
0\\
1
\end{array}\end{bmatrix} a\\
\\\therefore 고유벡터 \; X &= \begin{bmatrix}\begin{array}{c}
0\\
1
\end{array}\end{bmatrix}
\end{align*}$$
{: .notice}

<br>그리고 $\lambda=3$일때,

$$\begin{align*}
(A-\lambda I)\times X &=(A-3I)\times X\\&=\begin{bmatrix}\begin{array}{cc}
3-3 & 0\\
8 & 1-3
\end{array}\end{bmatrix}\times\begin{bmatrix}\begin{array}{c}
a\\
b
\end{array}\end{bmatrix}=0\\&=\begin{bmatrix}\begin{array}{cc}
0 & 0\\
8 & -2
\end{array}\end{bmatrix}\times\begin{bmatrix}\begin{array}{c}
a\\
b
\end{array}\end{bmatrix}=0\\
\\\Rightarrow 8a-2b &= 0 \Leftrightarrow 8a = 2b \\\therefore b = 4a
\\\Rightarrow X &= \begin{bmatrix}\begin{array}{c}
a\\
b
\end{array}\end{bmatrix}= \begin{bmatrix}\begin{array}{c}
a\\
4a
\end{array}\end{bmatrix}= \begin{bmatrix}\begin{array}{c}
1\\
4
\end{array}\end{bmatrix} a\\
\\\therefore 고유벡터 \; X = \begin{bmatrix}\begin{array}{c}
1\\
4
\end{array}\end{bmatrix}
\end{align*}$$
{: .notice}


---
## Step 3: 결론
정리해보자면 아래와 같다.

**고유값 방정식:** <br>$A\lambda=\lambda X$ <br><br> **벡터**$\times$**행렬**을 하면 **크기**와 **방향**이 모두 바뀌는 것이 일반적이다. <br> 다만, 행렬의 **고유벡터**$\times$**행렬**이라면 **크기**만 바뀌고 방향은 바뀌지 않는다.
{: .notice--info}


