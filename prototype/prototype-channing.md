# Prototype Channing

아까 그 그림을 가져와보면 

![](../.gitbook/assets/image%20%2825%29.png)

배열 리터럴은 Array생성자 함수와 그 prototype으로 이루어져 있죠? 

그리고 Array의 prototype은 객체이죠. 

`__proto__`는 생략이 가능하기 때문에 배열 instance 즉, `[1,2,3]`이 마치 자신의 메소드인것 처럼 prototype 메소드를 호출할 수 있죠?

그런데 이 prototype이 객체라는 말은 곧 Object생성자함수의 new 연산자로 생성된 instance라고 할수 있겠죠? 

그리고 또 마치 Object생성자의 prototype또한 자신의 메소드 인것처럼 사용할 수 있습니다. 아래 그림처럼 말이죠!!

![](../.gitbook/assets/image%20%2835%29.png)

이처럼 \_\_proto\_\_라는 붉은 점선을 따라 연결된 것을 바로 **prototype channing** 이라고 합니다.

{% hint style="info" %}
prototype은 모두 객체이기 때문에 모든 데이터 타입은 이와 동일한 구조를 따릅니다. 
{% endhint %}

숫자 리터럴도 한번 살펴볼까요? 

![](../.gitbook/assets/image%20%2820%29.png)

숫자 리터럴은 객체가 아니기 때문에 \_\_proto\_\_ 프로퍼티가 있을수는 없지만, 사용자가 이 숫자 리터럴을 객체인것 처럼 

즉, 메소드를 사용하려고 한다면 자바스크립트는 자동으로 숫자 리터럴을 Number생성자 함수의 instance로 변환합니다. 

이밖에도 문자열, 불린, 함수, 정규표현식 모두 이와 같은 생성자 함수가 존재하며 각 생성자 함수의 prototype에는 각 데이터 타입마다 필요로 하는 메소드가 정의 되어 있습니다. 

![&#xC774;&#xB807;&#xAC8C; &#xB9D0;&#xC774;&#xC8E0; ](../.gitbook/assets/image%20%2828%29.png)

그리고 모든 데이터 타입에 있는 prototype에 연결된 Object.prototype에는 자바스크립트전체에 사용할수 있는 hasOwnProperty\(\)와 같은 메소드들이 정의되어 있습니다. 

![](../.gitbook/assets/image%20%2823%29.png)

이렇게 Object.prototype에 정의된 메소드에는 모든 데이터 타입이 접근이 가능하겠죠? prototype객체는 모든 객체에 존재하기 때문에.

그래서 진짜 객체 데이터의 경우에는 좀 화가 납니다. 

왜냐하면 아래 그림처럼 객체데이터를 위한 prototype메소드를 정의해 둘 수 없기 때문이죠. 

![](../.gitbook/assets/image%20%2817%29.png)

 객체에 있는 prototype메소드들은 다른 모든 데이터 타입도 적용되기 때문입니다. 

객체입장에서도 다른 데이터 타입처럼 자신만의 메소드를 정의하고 싶지만 그렇자니, 다른 데이터들도 모두 접근이 가능해지기 때문에 그럴수가 없습니다.. 

그래서 어쩔수 없이 객체 생성자 함수에 직접 메소드들을 정의할 수밖에 없었습니다. 

![&#xC67C;&#xCABD;&#xC774; &#xAC1D;&#xCCB4;&#xB97C; &#xC704;&#xD55C; &#xB9E4;&#xC18C;&#xB4DC;](../.gitbook/assets/image%20%2824%29.png)

{% hint style="info" %}
유독 객체리터럴에 이상하게 Object.\*\*\* 들이 많이 등장하는 이유가 바로 이 상속구조 때문입니다. 
{% endhint %}



## Prototype Channing활용

```javascript
var arr = [1,2,3];
console.log(arr.toString()); //'1','2','3'
```

배열에는 toString\(\)이라는 메소드가 없지만 toString메소드를 사용하면 값이 잘 출력됩니다. 

만약 내용은 다르지만 이름이 같은 메소드를 직접 할당하면 어떻게 될까요? 

```javascript
var arr = [1,2,3];
arr.toString = function(){
	return this.join('_');
}
console.log(arr.toString()); //'1_2_3'
```

이렇게 되면 직접 정의한 메소드를 사용하게 됩니다. 



이번에는 좀 다양한 프로토 타입에 접근을 해보겠습니다. 

단 `call`을 이용해 명시적으로 **this를 바인딩** 해준뒤 실행하겠습니다.

```javascript
var arr = [1,2,3];
arr.toString = function(){
	return this.join('_');
}
console.log(arr.toString()); 
//'1_2_3'

console.log(arr.__proto__.toString.call(arr)); 
//1,2,3

console.log(arr.__proto__.__proto__.toString.call(arr));
//[object Array]
```

* 첫번째 값은 배열에 직접만든 메소드가 사용되었고
* 두번째는 prototype의 메소드가 사용되었습니다. 

첫번째 값과 두번째 값을 같게 만들어 보아요. 

```javascript
var arr = [1,2,3];
arr.prototype.toString = function(){
	return '[' + this.join(',') + ']';
}
console.log(arr.toString()); 
//'[1,2,3]'

console.log(arr.__proto__.toString.call(arr));
//'[1,2,3]'

console.log(arr.__proto__.__proto__.toString.call(arr));
//[object Array]
```



이번에는 객체를 살펴볼까요? 

```javascript
var obj = {
	a:1,
	b:{
		c:'c'
	}
};
console.log(obj.toString())
//[object Object]
```

좀전에 위에 배열도 object.toString을 하니 이런 모양이 나왔는데, 객체용 메소드가 아니라 그런것 같습니다. 

직접 한번 만들어 보겠습니다. 

![&#xC6B0;&#xCE21; &#xC0C1;&#xB2E8;&#xC774; &#xC2E4;&#xD589;&#xACB0;&#xACFC;](../.gitbook/assets/image%20%2811%29.png)

결과가 마음에 들지 않습니다. 

* b는 객체가 담겨서 출력되었고,
* 의도치 않게 toString 메소드 까지 모두 출력이 되었습니다. 

위 toString 메소드를 prototype으로 옮겨 보겠습니다.

![&#xB2E8;&#xC9C0; prototype&#xC548;&#xC5D0; &#xB123;&#xC5B4;&#xC8FC;&#xB294;&#xAC83; &#xB9CC;&#xC73C;&#xB85C; &#xACB0;&#xACFC;&#xAC00; &#xC798; &#xB098;&#xC654;&#xC2B5;&#xB2C8;&#xB2E4;.](../.gitbook/assets/image%20%2876%29.png)

이제 배열과 객체 함수가 모두 합쳐진 객체도 예쁘게 출력되게 만들 수 있을 것 같습니다.

![](../.gitbook/assets/image%20%2818%29.png)

다음에는 이 Prototype Channing을 활용해 Class를 만드는 법을 알아보겠습니다. 

