---
layout: single
title: "[알고리즘] Union and Find [C++]"
# 카테고리 작성
categories: [Alogrithm]
# 태그 작성, 여려개 작성할시에 []안에 쉼표로 구분
tag: Union and Find
# 마크다운의 '#'갯수에 [백준, 알고리즘따라 오른쪽에 목차 설정
toc: true
# 게시글에서 옆에 프로필 보이는지
author_profile: false
# 사이드바 설정
sidebar:
  nav: "docs"
---

## 설명

<span style="font-size:90%">
서로소 집합을 표현하는 알고리즘이다.\\
여러개의 원소들을 트리형태로 연결시켜서 같은 집합인지 판단한다.\\
unf라는 배열은 원소들의 연결 상태를 나타내는 배열인데, index는 원소이고 배열의 값은 index와 연결된 원소를 의미한다.\\
Find함수는 원소와 연결된 원소들을 끝까지 타고 들어가서 끝에 있는 원소를 반환한다.\\
Union은 Find가 반환한 값들(끝 원소)이 같은지 판단해서 값이 다른경우에 같은 집합으로 만들어 준다.\\
결국 각 원소들과 연결된 끝 원소들로 같은 집합에 속하는지 판단한다.\\
</span>

## 시간 단축

<span style="font-size:90%">
Union and Find를 이용하여 백준에서 알고리즘을 풀던 도중 계속 시간초과가 발생하는 경우가 생겼다.\\
원인을 찾다보니 결국 한줄 차이였다.\\
40번 라인을\\
return Find(unf[element]); 에서\\
return unf[element] = Find(unf[element]); 로 바꾸니 해결되었다.\\
\\
이 둘의 차이에 대해서 알아보자.\\
return Find(unf[element]); 인 경우에는 \\
연결 상태가 1-2-3-4-5 이렇게 되어 있을것이다\\
Find(1)로 시작되면 2,3,4를 거쳐 결국 Find(5) 까지 호출이 되어야 해서 시간적으로도 공간적으로도 비효율적으로 보인다.\\
배열의 상태는 이럴것이다.\\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;index : 1 2 3 4 5\\
unf[index] : 2 3 4 5 5<br><br>
return unf[element] = Find(unf[element]); 인 경우에는 \\
함수가 재귀적으로 호출되면서 unf[element]의 값을 변경시켜 준다.\\
그러면 1,2,3,4 가 바로 5와 연결되는 그림이 된다.\\
(5의 자식노드로 1,2,3,4 가 있는 그림이 된다.)\\
그러면 Find(1)=5 이므로 Find(5)가 호출되고 Find(5)==5 이므로 2,3,4를 거치지 않고 바로 5로 뛰어넘어서 끝 노드를 알 수있다.\\
배열의 상태는 이럴것이다.\\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;index : 1 2 3 4 5\\
unf[index] : 5 5 5 5 5
</span>

```c++
int unf[100001];

int Find(int element) {
if(node==unf[element]) {
return element;
}else {
return unf[element] = Find(unf[element]);
}
}

void Union(int element1, int element2) {
element1 = Find(element1);
element2 = Find(element2);

    if(element1 != element2) {
    	unf[element1] = element2;
    }

}

```

```

```
