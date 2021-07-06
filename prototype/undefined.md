# 메소드 상속 및 동작원리

아래 코드를 봐주세요

![](../.gitbook/assets/image%20%2865%29.png)

**Person 생성자**로부터 gomu와 iu라는 **두개의 instance**를 만들었고 각각 `setOlder` /`setAge`메소드를 만들어 주었습니다.

두 메소드는 완전 동일한 내용으로 이루어져 있는데 반복되고 있습니다. 

이걸 어떻게 해야 할까요? 

프로토타입으로 두 메소드를 이동시켜보겠습니다.

![](../.gitbook/assets/image%20%2840%29.png)

그러면 각 instance에서 \_\_proto\_\_ 를통해 메소드에 접근이 가능해지겠죠? 아래와 같이

```javascript
gomu.__proto__.setOlder();
gomu.__proto__.setAge();
```

{% hint style="danger" %}
하지만 이런 방법으로 접근하게 되면 앞서 살펴본 메소드의 this는 \_\_proto\_\_를 가리키기 때문에 NaN이 출력이 될 것입니다. 
{% endhint %}

하지만!! 

`__proto__`는 생략이 가능하기 때문에 다음과 같이 사용할 수 있습니다. 

```javascript
gomu.setOlder();
gomu.setAge();
```

마치 자신의 것처럼 메소드를 호출할 수 있게 해주고 이렇게 되면 두 메소드의 this는 gomu를 바라보게 되겠죠. 

그런데 생성자 함수에 age라는 프로퍼티가 이미 존재 했다면 결과는 달라지게 됩니다. 

`Person.prototype.age = 100;` 이었다고 가정해보겠습니다.

![\_\_proto\_\_&#xB294; prototype&#xC758; instance&#xC548;&#xC5D0;&#xC11C;&#xC758; &#xC774;&#xB984;&#xC774;&#xC5C8;&#xC8E0;? ](../.gitbook/assets/image%20%2862%29.png)

그렇게 되면 `gomu.__proto__.setAge();` 는 `setAge`의 **this**즉 **prototype의 age**에 **+1** 되서 101이 출력되게 되는 것입니다.  

당연한 결과이죠?? 다음에는 prototype channing을 배워보아요.

