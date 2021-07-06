# 함수Scope & 실행 Context

## Function Scope & Execution Context

### 정의

* 스코프\(Scope\) - 유효범위 \(변수\)
* 실행 컨텍스트 - 실행되는 코드덩어리 \(추상적 개념\)

### 차이점

둘의 가장 큰 차이는 각각 발생하는 시점에 있는데, 

* 스코프는 함수가 '**정의'**될때 결정되지만, 
* 실행 컨텍스트에는 함수가 '**실행'**될때 결정됩니다. 

실행 컨텍스트는 **호이스팅 / this바인딩** 등의 정보가 담기게 됩니다.

즉, 사용자가 함수를 실행했을때 외부적으로 함수가 실행되는데 필요한 환경등의 정보를 볼러 모아놓은 집합체인 것입니다. 

사실 개념보다는 이해가 중요하기 때문에 실제 코드를 보고 한번 살펴볼까요? 

#### 아래 코드에서 `console.log()`가실행되는 순서를 먼저 생각해보세요. 

```javascript
var a= 1;
function outer(){
	console.log(a);

	function inner(){
		console.log(a);
		var a = 3;
	}

	inner();

	console.log(a);
}
outer();
console.log(a);
```



예측이 완료되었나요?

함수선언과 호출의 차이를 알고있기 때문에 그냥 위에 console.log부터 실행이 될것입니다. 

#### 어떤 값이 출력되는지도 예측해보세요. 

```javascript
var a= 1;
function outer(){
	console.log(a);  //1. 1

	function inner(){
		console.log(a);//2. undifined
		var a = 3;
	}

	inner();

	console.log(a);  //3. 1
}
outer();
console.log(a);    //4. 1
```

실행되는 순서는 다음과 같습니다.

1. 전역 실행컨텍스트 생성 \[GLOBAL\]
2. 호이스팅 처리

   변수 a 선언

   함수 outer선언\[GLOBAL &gt; outer\] - 호이스팅 종료

3. outer함수 호출 
   1. outer실행 컨텍스트 생성
   2. 호이스팅 처리

      함수 inner 선언 \[GLOBAL &gt; outer &gt; inner\]

      outer scope에서 a탐색 -&gt; global scope에서 a탐색 -&gt; 1출력

   3. inner함수 호출
      1. inner실행 컨텍스트 생성
      2. 변수 a선언
      3. inner scope에서 a탐색-&gt; undifined출력
      4. 변수a에 3할당
   4. inner실행 컨텍스트 종료
   5. outer scope에서 a탐색 -&gt; golbal scope에서 a 탐색 -&gt;1출력
4. outer실행 컨텍스트 종료
5. global scope에서 a탐색 -&gt; 1출력
6. 전역 실행컨텍스트 종료

![](../.gitbook/assets/image%20%284%29.png)

