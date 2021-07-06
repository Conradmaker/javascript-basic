# Closure로 PrivateMember만들기

Java등의 여러 언어에는 매소드나 프로퍼티를 Private하게 만들수 있는 기능들이 내장되어 있습니다. 

Javascript에는 그런 기능은 없지만 Closure를 이용해 비슷하게 만들 수는 있습니다. 

Private Member를 만드는 것은 

* 첫번째로 외부로부터의 접근을 제한하는 것 뿐만 아니라, 
* 두번째로 전역Scope의 변수를 최소화 하는것에도 도움이 됩니다. 



이번에는 자동차 게임을 만들면서 이해해 보면 좋을 것 같습니다. 

* 차량별로 **연료**량 및 **연비**는 랜덤
* 유저별로 차량 하나씩 고르면 게임 시작
* 각 유저는 자신의 턴에 주사위를 굴려 랜덤하게 나온 **수만큼 이동**
* 만약 연료가 부족하면 **이동 불가**
* 가장 멀리 간 사람이 승리

이걸 구현하기 위해 먼저 차량 한대의 기능을 만들어 보아야 할것 같습니다.

```javascript
var car = {
	fuel:10, //연료(l)
	power:2, //연비(km/l)
	total:0,
	run:function(km){
		var wasteFuel = km/this.power;
		if(this.fuel<wasteFuel){
			console.log('이동불가');
			return;
		}
		this.fuel -= wasteFuel;
		this.total += km;
	}
}
```

* car 라는 객체 안에 fuel / power / total 프로퍼티를 넣고
* run 매소드 내부에서 이동 가능한지를 판단하고 fuel과 total을 반환합니다. 

이러한 경우에는 기능은 작동이 되겠지만, 문제가 하나 있습니다. 

{% hint style="danger" %}
아래와 같이 외부에서 내마음대로 값을 변경해 치트키를 쓸 수도 있기 때문입니다. 

```javascript
car.power = 10;
car.fuel = 1000;
```
{% endhint %}

따라서 안정적인 서비스를 위해서는 직접적으로 변경할 수 없게 만들면 되겠죠?

Scope를 활용해 외부에서 접근을 막고 싶은 변수를 지역변수로 만들고, 외부에 노출할 기능만을 return 하면 되겠죠!!

```javascript
var createCar = function(f,p){
	var fuel = f;
	var power = p;
	var total = 0;
	return {
		run:function(km){
			var wasteFuel = km/power;
			if(fuel<wasteFuel){
				console.log('이동불가');
				return;
			}
			fuel -= wasteFuel;
			total += km;
		}
	}
};
var car = createCar(10,2);
```

* fuel / power / total을 지역변수로 감추고,
* 외부로는 run이라는 매소드만을 노출시켰습니다. 

이렇게 하면 연료나 연비를 외부에서 알수도 없으며, 외부에서 값을 변경시킬수도 없습니다. 

사용자는 오직 run이라는 매소드만을 사용할수 있는 것이죠. 

closure를 활용해 private멤버와 public멤버를 구분하는 방법은 다음과 같습니다.

1. 함수에서 지역변수 및 내부함수 등을 생성한다. 
2. 외부에 노출시키고자 하는 멤버들로 구성된 객체를 return한다.

   -&gt;**return한 객체에 포함되지 않는 멤버들은 private하다.** 

   -&gt;**return한 객체에 포함된 맴버들은 public하다**

### **정리**

return function - 최초선언시의 정보를 유지 

함수 내부에서 다시 함수를 return하면 return된 함수는 그 함수가 최초 선언될 당시 정보를 유지합니다. 

그렇기 때문에 외부에 노출하고자 하는 데이터만 return하게 되면

그로인해 return하지 않은 데이터는 

* 접근 권한 제어
* 지역변수 보호
* 데이터 보존 및 활용

이라는 이점을 가질 수 있게 되는 것입니다. 

closure는 객체지향 프로그래밍이나 함수형 프로그래밍의 currying을 위해서 반드시 알아야 하는 개념이기 때문에 꼭 알고 넘어가야 한다고 생각합니다. 

