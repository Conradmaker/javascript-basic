# Prototype과 constructor , \_\_proto\_\_

![&#xC774; &#xADF8;&#xB9BC;&#xC740; Prototype&#xC744; &#xC774;&#xD574;&#xD558;&#xAE30;&#xC5D0; &#xC55E;&#xC73C;&#xB85C; &#xB4F1;&#xC7A5;&#xD558;&#xAC8C; &#xB420; &#xADF8;&#xB9BC;&#xC785;&#xB2C8;&#xB2E4;. ](../.gitbook/assets/image%20%2886%29.png)

![](../.gitbook/assets/image%20%2873%29.png)

* 생성자 함수가 있을때 
* new 연산자를 써서 
* instance를 만들면
* 생성자 함수의 prototype이라고 하는 프로퍼티가
* \_\_proto\_\_  라는 프로퍼티에 전달이 됩니다. 

즉 생성자 함수의 Prototype과 Instance의 \_\_proto\_\_라는 프로퍼티는 같은 객체를 참조합니다. 

그런데 \_\_proto\_\_ 프로퍼티는 내부 프로퍼티에 접근할때 \_\_proto\_\_라는 단어를 생략할수 있기 때문에 다음과 같이 "표현" 할 수도 있습니다. 

![](../.gitbook/assets/image%20%2814%29.png)

다른예제를 보겠습니다. 

![](../.gitbook/assets/image%20%287%29.png)

1. 아래 배열이 있습니다.
2. 생성자로 생성하거나 리터럴로 생성해도 내부구조는 동일하지만 생성자의 경우로 보면 Array라는 생성자 함수에는  from\(\)과 같은 프로퍼티들이 있습니다. 
3. 아래그림 오른쪽 콘솔은 개발자도구에서 `console.dir(Array)`를 출력한 결과입니다.
4. 이중에 prototype이라는 프로퍼티가 배열에 \_\_proto\_\_에 연결되어 있습니다. 
5. 그리고 그 prototype 프로퍼티는 객체이며 concat\(\)과 같은 것이 담겨있습니다. 즉 배열 매소드가 들어있습니다. 

![](../.gitbook/assets/image%20%281%29.png)

위에 위에 사진을 도식화하면 아까 봤던 이그림이 나오게 됩니다. 

![](../.gitbook/assets/image%20%2839%29.png)



배열 리터럴을 출력해볼까요? 

![](../.gitbook/assets/image%20%2866%29.png)

모두 알고 있을 length 프로퍼티와 함께 \_\_proto\_\_ 프로퍼티 가 함께 나옵니다. 

색이 다른 이유는 JS안에서 자동으로 생성되는 프로퍼티이기 때문에 구분을 위함입니다. 

여기서 \_\_proto\_\_를 열어보면 아까 본 그 매소드들이 나오게 됩니다. 

![&#xADFC;&#xB370; \_\_proto\_\_&#xC548;&#xC5D0; constructor&#xD504;&#xB85C;&#xD37C;&#xD2F0;&#xAC00; &#xC788;&#xB294;&#xB370; &#xB2E4;&#xC2DC; Array&#xAC00; &#xB2F4;&#xACA8;&#xC788;&#xC5B4;&#xC694;..](../.gitbook/assets/image%20%2838%29.png)

배열에는 분명히 constructor가 없음에도 Array가 출력이 되는데 

배열의 \_\_proto\_\_.constructor도 같이 Array가 출력이 됩니다.

![\_\_proto\_\_&#xAC00; &#xC0DD;&#xB7B5; &#xAC00;&#xB2A5;&#xD558;&#xB2E4;&#xB294; &#xC99D;&#xAC70;&#xC785;&#xB2C8;&#xB2E4;!!](../.gitbook/assets/image%20%2889%29.png)



다음 코드들은 모두 같은 gomu의 constructor를 가리키고 있습니다. 

![](../.gitbook/assets/image%20%2852%29.png)

즉 아래 4가지 방식은 모두 같은 생성자 함수의 prototype에 접근이 가능하며, 

* `[CONSTRUCTOR].prototype`
* `[instance].__proto__`
* `[instance]`
* `Object.getPrototypeOf([instance])`

위 코드처럼 아래 5가지 방식으로 생성자 함수에 접근할 수 있는 것입니다.

* `[CONSTRUCTOR]`
* `[CONSTRUCTOR].prototype.constructor`
* `(Object.getPrototypeOg([instanve])).constructor`
* `[instance].__proto__.constructor`
* `[instance].constructor`

이게 프로토타입에 대한 전부입니다!

