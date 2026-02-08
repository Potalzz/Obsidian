
`float4` = swift로 치면 `SIMD4<float>`와 같음.

자주 사용하는 `fixed`, `half`, `float`를 보자.
`fixed`는 정밀도가 매우 낮아(-2 ~ 2)주로 color에 사용된다.
`half`는 중간 정밀도
`float`는 `float`로 가장 높은 정밀도를 가짐.

정밀도 순서
`float` > `half` > `fixed`


---

`UnityObjectToClipPos()`
인자로 받은 값에 MVP(Model, View, Projection)행렬을 곱해주는 유니티 내장 메서드
