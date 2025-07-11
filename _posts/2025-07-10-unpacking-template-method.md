---
title: "[디자인 패턴 시리즈] Template Method 파헤치기"
excerpt: "디자인 패턴 중 하나인 Template Method의 배경과 개념, 원칙을 예제로 알아봅니다."

categories:
  - unpacking
tags: ["디자인패턴", "템플릿 메서드", "Java 언어로 배우는 디자인 패턴 입문", "쉽게 배워 바로 써먹는 디자인 패턴"]

permalink: /unpacking/template-method/

toc: true
toc_sticky: true

date: 2025-07-10
last_modified_at: 2025-07-10
---


# 🧱 Template Method 패턴 파헤치기

##  왜 만들어졌을까요?

사람은 지식을 추상화해서 배웁니다.
예를 들어, 누군가가 샌드위치를 만드는 과정을 보면, 그 사람이 어떤 재료를 넣었는지보다 '샌드위치를 이렇게 만드는구나'라는 **절차적 흐름**을 기억하게 됩니다.

막상 샌드위치를 직접 만들려고 하면, '샌드위치를 만드는 법'이라는 **공통된 방식**만 떠올리고, 재료나 세부 단계는 스스로 결정하게 됩니다.

이처럼 **공통된 흐름과 각자 다른 세부 구현**이 있는 상황은 소프트웨어 설계에서도 자주 나타나며, 이를 효과적으로 관리하기 위해 **Template Method 패턴**이 만들어졌습니다.

---

##  Template Method 패턴이란?

Template Method 패턴은 **공통 로직은 상위 클래스**에 두고,
**변경 가능하거나 구체적인 구현은 하위 클래스**에 맡기는 패턴입니다.

예를 들어 샌드위치를 만든다고 할 때,

* '빵을 자르고',
* '속재료를 넣고',
* '다시 빵을 덮는'

이런 **공통된 과정은 상위 클래스**에 정의합니다.
하지만 어떤 속재료를 넣을지는 하위 클래스가 결정하게 됩니다.

상위 클래스에서는 하위 클래스가 구현할 메서드를 **호출만** 하고,
구현은 하지 않습니다. 이런 메서드는 주로 `abstract` 키워드를 사용해서 정의합니다.
사용자는 공통 로직인 템플릿만 호출하면 되기 때문에, 하위 클래스로의 불필요한 접근은 접근제어자를 `protected`를 부여하여 제한합니다.
또한, 하위 클래스가 함부로 상위 클래스의 공통 로직을 변경하지 못하도록, 상위 클래스의 메서드에는 `final` 키워드를 붙여서 **오버라이딩을 막습니다**.


---

##  예시 코드

```java
// 상위 클래스
abstract class SandwichMaker {

    public final void makeSandwich() {
        cutBread();
        addIngredients();
        addSauce();
        wrapUp();
    }

    protected abstract void cutBread();
    protected abstract void addIngredients();
    protected abstract void addSauce();

    protected void wrapUp() {
        System.out.println("샌드위치를 포장합니다.");
    }
}

// 하위 클래스
class VeggieSandwich extends SandwichMaker {

    @Override
    protected void cutBread() {
        System.out.println("통밀빵을 반으로 자릅니다.");
    }

    @Override
    protected void addIngredients() {
        System.out.println("양상추, 토마토를 넣습니다.");
    }

    @Override
    protected void addSauce() {
        System.out.println("머스타드 소스를 뿌립니다.");
    }
}
```

---

##  어떤 원칙이 적용되나요?

### 1. 헐리우드 원칙 (Hollywood Principle)

> “Don’t call us, we’ll call you.”

상위 클래스는 구체적인 처리를 하위 클래스에게 맡깁니다.
즉, **상위 클래스가 하위 클래스를 호출**하지, 하위 클래스가 상위를 직접 제어하지 않습니다.
이렇게 설계하면 **의존성 역전**이 자연스럽게 적용됩니다.

### 2. 리스코프 치환 원칙 (Liskov Substitution Principle)

하위 클래스는 언제든지 상위 클래스의 역할을 대체할 수 있어야 합니다.
즉, `SandwichMaker` 타입의 참조 변수에 어떤 하위 클래스를 넣더라도 제대로 동작해야 합니다.

---

##  실제 적용 예: `java.io.InputStream`

Java의 `InputStream` 클래스도 Template Method 패턴을 활용하고 있습니다.

예를 들어, `read(byte[] b, int off, int len)` 메서드는 **1바이트씩 읽는 `read()` 메서드를 호출하는 방식**으로 구현되어 있습니다.
즉, 상위 클래스인 `InputStream`이 **템플릿 메서드**를 제공하고,
하위 클래스에서 `read()` 메서드를 구현함으로써 전체 로직이 동작하도록 합니다.

---

## 마무리

Template Method 패턴은 공통 로직을 재사용하면서도,
변경이 필요한 부분은 유연하게 확장할 수 있도록 돕는 대표적인 객체지향 설계 패턴입니다.

* 변경이 잦은 부분은 하위 클래스에서 구현하게 하고
* 변경되지 않는 흐름은 상위 클래스에서 고정시켜
  **확장성과 안정성을 모두 확보할 수 있습니다.**

앞으로 공통된 프로세스를 가진 기능을 구현할 일이 생긴다면
Template Method 패턴을 고려해보시길 추천드립니다.
