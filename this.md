# this

this는 처음에 모두가 어렵다고 느끼는 부분입니다. 

하지만 이것만 알면 다 됩니다. 

아래 상황시에 this가 무엇을 가리키는지만 알면 this를 이해할 수있습니다.

* 전역공간
* 함수내부
* 메소드 호출시
* callback
* 생성자함수

## 전역공간

![&#xC804;&#xC5ED;&#xACF5;&#xAC04;&#xC5D0;&#xC11C; this&#xB294; golbal&#xAC1D;&#xCCB4;&#xB97C; &#xAC00;&#xB9AC;&#xD0B5;&#xB2C8;&#xB2E4;.](.gitbook/assets/image%20%2875%29.png)

window와 global은 ECMA script에서 정의한 구현체입니다. 

정의한 바에따라 구체적인 내용이 달라지는 것이죠.



## 함수내부

아래 있는 모든 함수내부에서 this는 전역객체를 가리킵니다.

![&#xBAA8;&#xB450; window&#xB97C; &#xCD9C;&#xB825;&#xD569;&#xB2C8;&#xB2E4;.](.gitbook/assets/image%20%2856%29.png)

함수내부에서 this는 **'기본적으로'** 전역객체를 가리키며 ,

**'default'**이기 때문에 이는 바뀔수 있습니다.



## 매소드 호출시

![](.gitbook/assets/image%20%2851%29.png)

매소드의 경우에는 호출된 매소드의 `.`앞에있는 객체가 this라고 할 수 있습니다.

쉽개 생각하기 위해서는 

{% hint style="info" %}
함수는 **\(전역객체의\)** 메소드다!
{% endhint %}

라고 생각하면 편할 수 있습니다.

### 내부함수에서의 우회법

매소드 안에서 내부함수가 있을경우 this가 문제가 될때가 있는데, 

![&#xC11C;&#xB85C; &#xB2E4;&#xB978; &#xAC12;&#xC744; &#xCD9C;&#xB825;&#xD558;&#xACE0; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.](.gitbook/assets/image%20%2855%29.png)

첫번째 `console.log()`는 **매소드로 호출**이 되었죠. 그래서 this는 obj를 가리키고 있어 20이 출력됩니다. 

두번째 `console.log()`는 **함수로 호출**되었기 때문에 전역객체 a 10을 가리키고 있습니다.

그렇다면 함수c에서도 20이 출력되게 obj를 this로 쓸수는 없을까요? 

![](.gitbook/assets/image%20%2868%29.png)

내부함수에서 self라는 변수를 활용하면 자신의 스코프에서 a를 찾다가 없으니 스코프체인을 타고 위로 올라가 a를 찾겠죠.

물론 취향에 따라 \_this, that, self로 사용할 수 있습니다. 



## callback에서

callback함수에서는 기본적으로 함수내부에서와 동일입니다. 

### call, apply, bind

이건 간단히 설명할수가 없습니다. 먼저 배경지식을 다루면

call, apply, bind 매소드를 알아보겠습니다. 

![&#xC704; &#xCF54;&#xB4DC;&#xB294; &#xBAA8;&#xB450; &#xB3D9;&#xC77C;&#xD55C; &#xACBD;&#xACFC;&#xB97C; &#xCD9C;&#xB825;&#xD569;&#xB2C8;&#xB2E4;. ](.gitbook/assets/image%20%2841%29.png)

공식문서를 살펴보면 다음과 같이 설명하고 있습니다.

![](.gitbook/assets/image%20%2822%29.png)

여기서 thisArg는 this를 이걸로 해줘 라고 개발자가 명시하는 것입니다.

* call,bind는 thisArg 이후로 인자를 무한으로 넣을수 있습니다. 

자 여기서 call을 살펴보면 위 코드중 `a.call(b,1,2,3);` 이코드를 보면 다음과 같이 해석할 수 있습니다.

> a함수를 호출하는데 this는 b로하고 인자로 1,2,3을 넘겨줘



* apply의 경우에는 두번째 인자로 배열이 오는데 배열안에 인자를 넣어주면 됩니다.

 `a.apply(b,[1,2,3]);` 이코드는 다음과 같이 해석할수 있겠죠.

> a함수를 호출하는데 this는 b로하고 인자로 1,2,3을 넘겨줘

네 맞습니다 결과는 같지만, 인자를 하나하나 넣어주느냐, 아니면 2번째 자리에 배열로 몽땅 넣어주느냐의 차이입니다. 



단, call/apply와 bind에는 차이점이 하나 있습니다. 

call관 apply는 즉시 호출하는 기능이지만 , bind의 경우에는 새로운 함수를 생성\(currying\) 즉 변수에 새로운 함수를 담을 수 있을뿐 호출을 담당하지는 않습니다.

```javascript
var b={
	c:'eee'
};

var c = a.bind(b);
c(1,2,3);

var d = a.bind(b,1,2);
d(3);
```

d는 다음의 해석을 할 수 있습니다.

* a를 가지고 새로운 함수를 만들어주는데
* this는 b가 되었으면 좋겠고 인자에는 1,2를 미리 넣어두지. 
* 새로만든 함수는 변수d에 담아주고!
* d\(3\)은 1,2를 인자로 받지 말고 새번째인자를 받아줘! 

그래서 결국 결과는 모두 같습니다.

### callback함수 this

본론으로 돌아가 callback에서 this는 어떻게 될까요? 

```javascript
var callback = function(){
	console.dir(this);  
};
//위에서는 당연히 함수이기 때문에 window를 가리킵니다.

var obj = {
	a:1,
	b:function(cb){
		cb();
	}
};
obj.b(callback);
//callback에 제어권을 넘겨받은 함수가 호출하면 다른결과가 출력되겠죠?
//obj가 출력됩니다. 
```



setTimeout의 경우 callback에 대한 this를 정의하지 않아서 window를 가리킵니다.

```javascript
var callback = function(){
	console.dir(this);
};

var obj = {
	a:1
};
setTimeout(callback,100);
```

이런 경우에 this는 window를 가리키겠죠. 

this를 바인딩 해주기 위해서는 다음과 같이 해주면 됩니다. 

```javascript
var callback = function(){
	console.dir(this);
};

var obj = {
	a:1
};
setTimeout(callback.bind(obj),100);
```

이렇게 해주면 this가 obj를 가리키겠죠. 

물론 bind매소드가 없던 시절에는 함수를 한번 더 감싸고 self를 이용했지만 이제는 그럴 필요는 없습니다. 

이제 저번에 addEventListner의 this가 왜 element를 가리키는지 알수 있겠죠? 

addEventListner내부에서 callback함수에 대한 this를 element객체로 바인딩했기 때문입니다. 

물론 다음과 같은 방법으로 직접 바인딩 해줄수도 있습니다. 

![bind&#xB9E4;&#xC18C;&#xB4DC;&#xB97C; &#xC774;&#xC6A9;&#xD574; &#xBC14;&#xC778;&#xB529;](.gitbook/assets/image%20%288%29.png)

### 정리

* 기본적으로는 함수의 this와 같다.
* 제어권을 가진 함수가 callback의 this를 명시한 경우 그에 따른다. 
* 개발자가 this를 바인딩해서 callback을 넘기면 그에 따른다. 

## 생성자 함수에서

인스턴스를 가리키는데 별도로 설명할 내용은 없습니다. 

![](.gitbook/assets/image%20%2860%29.png)



## 정리

![](.gitbook/assets/image%20%2847%29.png)



