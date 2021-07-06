# Data type

## Data종류

자바스크립트의 Data type 은 크게 두가지로 분류할수 있습니다. 

* Primitive Type  \(원시형\)
* Reference Type  \(참조형\)

원시형 데이터에는 총 6가지 타입이 존재하죠.

1. Number
2. String
3. Boolean
4. null
5. undifined
6. symbol \(es6+\)

참조형 데이터에는 크게 객체\(Object\)가 있고 그 하위로 Array , Function , RegExp로 나누어지며,

es6에서는 map/set/weakMap/weakSet 등이 추가되었죠.

## 변수를 메모리에 할당하는 방법

### 원시형데이터

1. 먼저 메모리에 데이터를 담을 공간을 확보한후
2. 확보된 공간의 주소값을 변수명과 매칭시키고
3. 그 주소에 데이터를 넣어줍니다. 

![](.gitbook/assets/image%20%2887%29.png)

공간을 확보하고 해당공간의 주소를 변수명과 매칭시키는 선언과정

해당변수가 가르키는 주소공간에 데이터를 저장하는 할당과정으로 나눌 수 있죠. 

만약 `b = 'abc'` 를 `b=false`로 바꾸면 어떻게 될까요? 

b라는 변수명은 할당된 주소가 있기 때문에 그 주소를 읽어 이동한 후 314번 공간에 false를 넣어줍니다.

그렇다면 var c = b; 이렇게 되면 어떻게 될까요? 

b를 먼저 읽어 314번에서 false를 읽은뒤 c라는 변수에 315번 주소를 할당한뒤 그곳에false를 저장합니다.

이렇게 대입된 기본형 데이터는 비교가 가능한데 315번 공간에 저장된 false와 314번 공간에 저장된 false는 완전히 같다고 할 수 있겠죠??

![&#xADF8;&#xB7FC; c&#xBCC0;&#xC218;&#xBA85;&#xC5D0; 20&#xC744; &#xD560;&#xB2F9;&#xD574; &#xBCF4;&#xC544;&#xC694;](.gitbook/assets/image%20%2812%29.png)

![false&#xB97C; 20&#xC73C;&#xB85C; &#xB36E;&#xC5B4; &#xC50C;&#xC6CC;&#xBC84;&#xB9BD;&#xB2C8;&#xB2E4;.](.gitbook/assets/image%20%2881%29.png)

이렇게 되면 b와 c는 완전히 다른 값이 되었다고 할 수 있겠죠?

참조형 데이터는 동작이 조금 다릅니다. 



### 참조형 데이터

참조형 데이터는 미리 공간을 확보하고 주소를 변수명과 일치시키는 선언과정은 똑같습니다.

 할당과정은 조금 다릅니다. 

참조형 데이터는 Property와 Data 즉, Key:value의 형식을 띄고 있는데, Key는 변수명과 같은 역할을 하고 있습니다. 

만약 아래와 같은 객체가 있다고 해봅시다. 

```javascript
var obj = {
    a:1,
    b:'b'
}
```

1. 413번 주소에 변수명 obj를 매칭시킨뒤
2. 각 Property와 Data를 매칭시킬 공간1011을 하나더 확보합니다.
3. a Property와 b Property를 할당할 공간 1012, 1013번 공간을 확보하고 주소를 1011에 매칭합니다. 
4. 1012 , 1013에 각각 원시형 데이터를 할당해줍니다. 
5. 413번 공간에 1011주소를 매칭시켜 줍니다.

![](.gitbook/assets/image%20%282%29.png)

즉, 참조형 데이터는 기본형 데이터들의 집합이라고 할 수 있겠죠?

그런데 `var obj2 = obj` 이렇게 같은 값을 할당하면 어떻게 될까요.

기본형 데이터와는 다르게 그냥 Property와 주소가 매칭된 공간을 매칭시켜 주기만 하면 되겠죠? 

![](.gitbook/assets/image%20%2880%29.png)

자 이렇게 되면 obj와 obj2는 완전히 같은 객체 1011을 참조하고 있게 되는 것입니다. 

참조형 데이터 안에 또다른 참조형 데이터가 있는 것을 nasted하다고 하는데 한번 보겠습니다.

![&#xC774;&#xB807;&#xAC8C; &#xACFC;&#xC815;&#xC740; &#xAC19;&#xC2B5;&#xB2C8;&#xB2E4;. ](.gitbook/assets/image%20%2877%29.png)

그런데 obj3.a = 'new' ; 이렇게 기본형 데이터를 넣으면 어떻게 될까요? 

![&#xCC38;&#xC870;&#xB41C; &#xC8FC;&#xC18C;&#xB97C; &#xAC00;&#xC9C0;&#xACE0; &#xC788;&#xB294; 1185&#xBC88;&#xC758; &#xB370;&#xC774;&#xD130;&#xB9CC; &#xAE30;&#xBCF8;&#xD615;&#xC73C;&#xB85C; &#xBC14;&#xB00C;&#xC5C8;&#xC2B5;&#xB2C8;&#xB2E4;.](.gitbook/assets/image%20%286%29.png)

이렇게 되면 1326, 1327,1328번데이터는 아무런 참조의 대상이 되지 않고 남게 되는데, 이런경우에는 Garbage Collector 의 대상이 되어 언젠가 사라지게 됩니다. 

