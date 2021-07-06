# Callback 함수

Callback 함수를 살펴볼까요? 

Callback을 call과 back으로 나누어 보겠습니다. 

* call - 부르다
* back - 뒤로

> something will **'call'** this function **'back'** sometime somehow

무언가가 이 함수를 어떻게 언제 호출할지는 몰라도어쨋든 실행해서 다시 돌려줄거야!

즉, 콜백함수는 **제어권**을 넘겨준다는 것입니다. 

그렇다면 누구에게 제어권을 넘겨주는 것일까요??  그건 뒤에서 다루어보도록 하겠습니다. 

아무튼 그 콜백함수를 어떻게 처리할지는 제어권을 받은 그 대상에 달려있게 되는 것입니다.

```javascript
setInterval(function(){
	console.log('1초마다 실행될 것임.');
},1000);
```

`setInterval()`은 두번째인자간격으로 함수를 호출해주는 주기함수입니다.  

* 주기함수 호출 - setInterval\(\)
* 인자1\(콜백함수\) - function\(\){}  
* 인자2\(주기ms\) - 1000

그러면 1초마다 한번씩 콜백함수가 실행되는 것입니다. 

즉, callback함수의 **제어권**을 setInterval로 넘겨주는 것입니다. 

위에 코드를 이해하기 쉽게 변수로 치환하게 되면 다음과 같을 것입니다.

```javascript
var cb = function(){
	console.log('1초마다 실행될 것임.');
};

setInterval(cb,1000);
```

setInterval\( callback , ms \)  setInterval제어하에 callback함수를 ms마다 실행시켜 줍니다.

### forEach

forEach함수로 예시를 들어볼까요? 

```javascript
var arr=[1,2,3,4,5];
var entries = [];

arr.forEach(function(v,i){
	entries.push([i,v,this[i]]);
},[10,20,30,40,50]);

console.log(entries)
```

* arr 배열을 순회하면서 callback함수를 실행하라고 하고 있습니다.
* this를 \[10,20,30,40,50\]으로 하라고 하고 있습니다.
* 결과에 대해 entries를 출력하라고 하고 있습니다.

결과는 다음과 같습니다.

```javascript
[[1,1,10],[1,2,20],[2,3,30],[3,4,40],[4,5,50]]
```

참고로 forEach의 사용방법은 다음과 같습니다.

* arr.forEach호출 \(.이 있으니 매소드겠죠?\)
* 인자1 - 콜백함수
* 인자2 - this로 인식할 대상 \(생략가능\)

{% embed url="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global\_Objects/Array/forEach" %}

forEach함수의 내부 동작은 다음과 같다고 할 수 있습니다

![](../.gitbook/assets/image%20%2857%29.png)

줄쳐진 부분이 this를 바인딩하는 핵심인데, 

callBack을 어떤시기에 어떻게 호출하고 어떻게 넘겨줄지 이미 forEach함수 안에 정의되어 있기 때문에 forEach함수 내부에 정의된 대로 사용할 수 밖에 없죠.

이해가 어려울수 있으니 다른 예제도 한번 볼까요?

```javascript
var arr = [1,2,3,4,5];
arr.forEach(function(index,value){
	console.log(index,value);
})
```

원래 forEach문에는 value,index순으로 인자가 들어가는데 그 반대로 하고 싶어서 이렇게 코드를 쓰면 원하는 결과가 출력될까요? 

당연히 그렇게 되지 않습니다. 이미 forEach함수는 내부 규칙이 정해져 있기 때문이죠. 

즉, 그 대상의 규칙을 따라야 하며 그렇지 않으면 원하지 않는 결과를 얻을 수밖에 없습니다. 



### EventHandler

![&#xC804;&#xD600; &#xC608;&#xCE21;&#xD560; &#xC218; &#xC5C6;&#xB294; &#xACB0;&#xACFC;&#xAC00; &#xCD9C;&#xB825;&#xB418;&#xC5C8;&#xC2B5;&#xB2C8;&#xB2E4;.](../.gitbook/assets/image%20%2864%29.png)

* this를 바인딩 하지 않아서 window가 나올것 같지만 div엘리먼트가 출력되었습니다.
* x에는 인자를 넣어주지 않았는데도 자동으로 mouseEvent가 담겨있죠.

모두 예상하지 못한 결과가 나왔지만, addEventLisner의 규칙에 이미 인자가 이벤트 객체로 하고 this는 이벤트 target으로 하라고 규칙이 되어있기 때문입니다.

### 콜백함수의 특징

다른 함수 A 의 매개변수로 콜백함수 B를 전달하면 A가 B의 **제어권**을 가지게 된다.

특별한 요청 bind가 없는한 A에 **미리 정해진 방식**에 따라 B를 호출한다.

미리 정해져있는 방식이란 **this**에 무엇을 바인딩할지, **매개변수**에는 어떤 값들을 저장할지, 어떤 **타이밍**에 콜백을 호출할지 등이다.

### 주의점

콜백함수는 **매소드가 아닌 함수**입니다.

![&#xBA54;&#xC18C;&#xB4DC;&#xB85C; &#xD638;&#xCD9C;&#xD558;&#xAC8C; &#xB418;&#xBA74; this&#xB294; obj&#xB97C; &#xAC00;&#xB974;&#xD0A4;&#xACA0;&#xC8E0;.](../.gitbook/assets/image%20%2884%29.png)

![&#xCF5C;&#xBC31;&#xD568;&#xC218;&#xB85C; &#xC804;&#xB2EC;&#xD55C; &#xACB0;&#xACFC;&#xC785;&#xB2C8;&#xB2E4;. ](../.gitbook/assets/image%20%2863%29.png)

하지만 `obj.logValues`를 `forEach()`로 넘기게 되면, 메소드로 넘어가는 것이 아닌 `obj.logValues`가 **가리키고 있는 함수**만 전달이 되고 **제어권**은 `forEach()`가 가지게 됩니다.

