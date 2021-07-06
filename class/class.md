# Class

## Class의 의미

사전에서는 class를 계급, 집단, 집합이라고 정의하고 있습니다.

풀어서 해석하면 다음과 같습니다

> 공통적인 속성을 모아 하나로 묶은 덩어리 라고 할 수 있습니다.

class와 함께 등장하는 용어로는 instance가 있는데 instance는 해당 클래스의 속성을 지닌 구체적인 객체입니다. 

실생활에서 예를 들어보겠습니다.

![](../.gitbook/assets/image%20%2846%29.png)

* 배 사과 감 오렌지 바나나가 있습니다. 
* 위 요소들은 모두 과일이라는 집단에 속합니다.
* 여기서 과일은 class이고 배, 사과 ,감 등은 instance입니다.  
* 그럼 또 과일은 음식이라는 집단에 속하게 됩니다. 
* 과일 class는 음식이라는 상위class에 속한 하위 class입니다. 
* 그런데 배는 과일이면서 음식이고, 사과, 오렌지 감 모두 마찬가지 입니다.
* 음식, 과일은 추상적인 개념이지만, 사과 배 등은 실제로 만질수도 먹을수도 있는 구체적인 대상입니다. 
* 여기서 구체적인 대상을 instance 추상적인 개념을 class라고 하는 것입니다. 

실생활에서는 하위 클래스부터 정의가 가능하지만, 프로그래밍 상에서는 다릅니다. 

프로그래밍에서는 상위에 클래스먼저 정의를 해주어야만, 하위클래스와 그 인스턴스를 생성할 수 있습니다. 

여기서 음식클래스와 과일클래스의 관계를 따져보면 다음과 같이 설명할 수 있습니다.

* 음식 즉, 상위클래스는 superclass라고 칭합니다.
* 과일 즉, 하위클래스는 subclass라고 칭합니다.

이런 내용은 다음 클래스 상속에서 다루기로 하고  지금은 단일클래스에 집중해 보아요. 

![](../.gitbook/assets/image%20%2883%29.png)

배열 리터럴을 생성하면 그 배열은 사실 Array라는 생성자 함수로 new 연산자를 통해 호출한 결과물과 같다고 했습니다. 

![](../.gitbook/assets/image%20%2815%29.png)

그중 배열 리터럴을 제외한 부분을 보면 그 부분이 일반적으로 Class의 역할을 하게 되는 것이죠. 

왜냐하면 Array라는 생성자함수는 그자체로 특별한 기능을 가지는 것이 아닌 new연산자를 통해 생성한 배열의 기능을 정의하는데 주력하기 때문입니다.

클래스를 통해 생성한 객체 여기서는 배열객체는 실제 코드상에서 다루고 쓸수있는 것입니다. 그리고 이게 바로 instance가 됩니다. 

앞에 그림중 class부분만 따로 보겠습니다. 

![](../.gitbook/assets/image%20%2853%29.png)

prototype프로퍼티 내부에 할당되지 않고 Array생성자 함수 내부에 직접 할당되어 있는 프로퍼티들을 **static methods / static properties**라고 칭합니다.

이것들은 Array생성자 함수를 new 연산자 없이 일급 객체인 함수로써 호출할때에만 의미가 있는 값들입니다. 

보통 해당 클래스 소속인 instance의 개별적 동작이 아닌 소속여부 확인등의 공동체적인 기능을 활용할때 static메소드를 활용합니다. 

반면 prototype내부에 정의된 메소드들을 prototype methods 라고 하는데 일반적으로 메소드라고만 하는 경우가 많습니다. 

**static methods / static properties 과 \(prototype\) methods 는 instance에서 직접 접근할 수 있는지의 여부가 다릅니다.** 

![](../.gitbook/assets/image%20%2829%29.png)

* prototype의 메소드들은 instance와 \_\_proto\_\_로 연결되어 있고 생략 가능하기 때문에 바로 접근이 가능한 반면
* static methods / static properties는 우회는 가능하지만 바로 접근할수가 없습니다.



다음 예제를 살펴볼까요

![](../.gitbook/assets/image%20%2859%29.png)

* `Person`이라는 생성자 함수가 있고
* `Person.getInformations`
* `Person.prototype.getName`
* `Person.getAge`
* 위 3가지 메소드를 정의했습니다. 

![](../.gitbook/assets/image%20%2813%29.png)

이중 Person.getInformations 는 Static 메소드이고 나머지 2개는 prototype 메소드입니다. 

이제 이걸로 고무라는 Person을 생성해 보겠습니다. 

![](../.gitbook/assets/image%20%2845%29.png)

* gomu.getName\(\) / gomu.getAge\(\)는 prototype메소드이기 때문에 직접 접근해서 출력이 가능합니다.
* 반면에 gomu.getInformations\(gomu\)는 gomu라는 instance를 통해 접근할 수 없고,
* Person이라는 생성자 함수를 통해 접근해 주어야 합니다. 



## 정리

* Class는 어떤 공통된 속성이나 기능을 정의한 **추상적인 개념**
* 이 **클래스에 속한 객체**를 **instance**라고 한다. 
* Class에는 instance가 **직접 접근할 수 없는** 클라스 자체에서 접근 가능한 **Static Member** 즉,  **static methods / static properties** 가 있으며,
* instance에서 **직접 접근이 가능한** prototype methods가 있다. 

