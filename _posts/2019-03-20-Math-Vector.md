---
layout: post
title: "Math - Vector"
description: ""
date: 2019-03-20 19:00:00+09:00
tags: [math]
comments: true
share: true
---

[TOC]



## 좌표와 벡터

좌표 : 어느 지점을 가리키는 위치 정보

벡터 : 이동량을 나타내는 형태가 없는 정보(보통 원점에서 나오는 화살표로 그린다)



## 좌표와 벡터의 연산

좌표 + 벡터 = 좌표를 벡터만큼 움직인 좌표

좌표 - 벡터 = 좌표를 벡터만큼 반대로 움직인 좌표

좌표A + 좌표B = 벡터

좌표A - 좌표B = (B에서 A로 향하는)벡터



벡터A + 벡터B = 벡터(A에서 B만큼 이동)

벡터A - 벡터B = 벡터(A에서 B만큼 반대로 이동)



좌표 * 스칼라 = (원점에서 스칼라 만큼 확대된) 좌표

좌표 / 스칼라 = (원점에서 스칼라 만큼 축소된) 좌표



벡터 * 스칼라 = (길이가 스칼라 만큼 확대된) 벡터

벡터 / 스칼라 = (길이가 스칼라 만큼 축소된) 벡터





## 벡터의 정규화

벡터의 길이를 1로 만드는 것
벡터의 크기가 1로 고정되고 방향 정보만 남아서 계산이 편해진다.
$$
\hat{v}:\text{정규화된 벡터}, {\lVert v \rVert}:\text{벡터의 길이}
$$

$$
\hat{v} = \frac{v}{\lVert v \rVert}
$$



### 벡터의 덧셈에 대한 항등원

- 다른 벡터와 더했을 때 값을 변경시키지 않는 벡터
- 모든 요소가 0인 벡터, 영벡터라고 한다.

$$
\vec{v}+\vec{e} = \vec{v}
$$

### 벡터의 덧셈에 대한 역원

- 더했을 때 항등원(영벡터)가 나오는 벡터

$$
\vec{AB}에\ 대한\ 역벡터를\ \vec{BA}라\ 할때\\
\vec{AB}+\vec{BA}=\vec{e}이면\\
\vec{BA}를\ \vec{AB}에\ 대한\ 역원(역벡터)라\ 한다.
$$



### 단위벡터

- 길이가 1인 벡터
- 벡터의 실수배(스칼라과 벡터의 곱)에 대한 항등원이다.

$$
\begin{equation*}
\| \hat{v} \| =\sqrt{v^{2}_{x} +v^{2}_{y}} =1
\end{equation*}
$$





## 피타고라스 삼각항등식(Pythagorean trigonometric identity)

> 빗변의 길이가 1인 직각삼각형에서 빗변과 인접면 사이의 내각을 θ라 할때

$$
(\sin\theta)^2+(\cos\theta^2) = 1
$$



## 코사인법칙
> 세변의 길이가 각각 a, b, c이고 b와 c의 내각이 θ인 삼각형

$$
a^2 = b^2+c^2-2bc\cos\theta
$$



## 피타고라스의 정리
피타고라스의 정리는 코사인법칙의 특수한 케이스이다. (θ가 90˚인 경우 cos(90˚)=0)
> 직각삼각형의 밑변, 높이, 빗변을 각각 a, b, c라 할때 빗변 c의 길이

$$
c=\sqrt{(a^2+b^2)}
$$



## 내적(Dot Product, Inner Product)
두 개의 벡터를 하나의 스칼라양으로 변환하는 연산



### 내적 공식 1

$$
a \cdot b = {\lVert a \rVert}{\lVert b \rVert} \cos\theta
$$



### 내적 공식 2
내적 공식 1을 전개하면 다음 식을 얻을 수 있다.

> 2D일 경우

$$
a \cdot b = a_xb_x + a_yb_y
$$



### 벡터 자신과의 내적은 벡터 크기의 제곱과 같다

> 벡터 자신과의 각은 0이므로 cos(0) = 1

$$
\begin{matrix}
a \cdot a &=& {\lVert a \rVert}{\lVert a \rVert} \cos\theta \\
&=& {\lVert a \rVert} \times {\lVert a \rVert} \times 1 \\ 
&=& {\lVert a \rVert}^2
\end{matrix}
$$




### 정규화된 벡터의 내적

$$
\begin{matrix}
\hat{a} \cdot \hat{b} &=& {\lVert \hat{a} \rVert}{\lVert \hat{b} \rVert} \cos\theta \\
&=& 1 \times 1 \times \cos\theta \\
&=& \cos\theta
\end{matrix}
$$



### 정규화된 벡터의 내적값의 의미
정규화된 두 벡터의 내적은 cos값이기 때문에 두 벡터의 사이각을 알 수 있다. 하지만 cos값은 0~π(180)이기 때문에 기준 벡터의 방향에서 다른 벡터가 앞인지 뒤인지만 알 수 있고 왼쪽인지 오른쪽인지 알 수 없다.

cos값으로 각을 얻으려면 acos을 사용하면 된다.

| a^ · b^ 의 내적 값 | 사이각 (acos(a^ · b^)) |             의미             |
| :----------------: | :--------------------: | :--------------------------: |
|         1          |           0            |        두 벡터가 평행        |
|        < 1         |      0 ~ π/2(90˚)      |     벡터가 앞쪽에 있다.      |
|         0          |        π (90˚)         |        두 벡터가 수직        |
|        < 0         |   π/2(90˚) ~ π(180˚)   |     벡터가 뒤쪽에 있다.      |
|         -1         |        π(180˚)         | 두 벡터가 반대 방향으로 평행 |



### 정규화되지 않은 벡터의 내적값의 의미
정규화되지 않은 벡터끼리의 내적은 사이각으로 사용할 수 없지만 앞인지 뒤인지 등의 대략적인 위치는 판단이 가능하다.

내적 공식에서 두 벡터의 길이의 곱에 cosθ 값을 곱하는데 벡터의 길이의 곱은 양에 대한 값이기 때문에 양수이고 부호를 결정하는 것은 cosθ 값이다. cosθ 값은 정규화된 벡터의 내적과 동일하기 때문에 이 값의 부호를 보고 벡터의 앞, 뒤 관계를 알 수 있다.

정규화를 하면 더 정교하게 알 수 있지만 단순히 앞, 뒤, 수직인지만 알고 싶을 경우 정규화로 인한 자원소모를 하지 않기 위함이다. (정규화 시 제곱근 연산을 하는데 제곱근 연산은 컴퓨터의 자원을 많이 소모한다)

| a · b 의 내적 값 |        의미         |
| :--------------: | :-----------------: |
|       > 0        | 벡터가 앞쪽에 있다. |
|        0         |   두 벡터가 수직    |
|       < 0        | 벡터가 뒤쪽에 있다. |



## 외적(Cross Product)

하나의 점에서 만나는 두 벡터 각각과 수직인 벡터

외적은 두 벡터가 만드는 평행사변형의 면적과 크기가 같은 벡터이다.



### 외적 구하기

하나의 선 위에 있지 않은 평면 위의 세 점(평면 위의 벡터2개)으로 외적을 구할 수 있다.

하나의 선 위에 있다면 영벡터가 나온다.
$$
\begin{matrix}
A \times B &=& (a_yb_z - a_zb_y, a_zb_x - a_xb_z, a_xb_y - a_yb_x)
\end{matrix}
$$


### 외적의 교환법칙

외적의 결과는 벡터인데 외적 연산의 순서가 바뀌면 벡터의 방향이 반대가 된다.
$$
\begin{matrix}
A \times B &=& (a_yb_z - a_zb_y, a_zb_x - a_xb_z, a_xb_y - a_yb_x) \\
B \times A &=& (b_ya_z - b_za_y, b_za_x - b_xa_z, b_xa_y - b_ya_x) \\
&& a_yb_z - a_zb_y \neq b_ya_z - b_za_y \\
&& \therefore A \times B \ne A \times B \\\\

&& a_yb_z - a_zb_y = b_ya_z - b_za_y \times -1 = b_za_y - b_ya_z  \\
&& \therefore A \times B = -(B \times A)

\end{matrix}
$$

### 외적 벡터의 방향

좌표계에 따라 달라진다.

- 왼손 좌표계 : 두 벡터가 만나는 점을 축으로 왼손으로 감싸쥐는 방향(시계방향)에서 엄지 방향
- 오른손 좌표계 : 두 벡터가 만나는 점을 축으로 오른손으로 감싸쥐는 방향(시계방향)에서 엄지 방향



### 외적 벡터의 길이

외적 벡터를 만드는 두 벡터의 길이는 외적 벡터의 방향에 영향을 주지 않는다.

또한 계산 과정에서 정규화된 외적 벡터를 얻을 수 없으므로 외적 벡터를 얻은 후에 정규화 시켜줘야한다.


