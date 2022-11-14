# 구조체 

구조체 <sup>struct</sup> 는 3가지 타입이 있고 `struct` 키워드로 정의합니다.

* 튜플 구조체 (이름있는 튜플)
* 전통적인 [C언어 스타일 구조체][c_struct]
* 유닛 구조체는 필드가 없으며, 제네릭에서 유용합니다.

```rust,editable
// 사용하지 않는 코드에 대한 경고를 숨기는 속성
#![allow(dead_code)]

#[derive(Debug)]
struct Person {
    name: String,
    age: u8,
}

// 유닛 구조체
struct Unit;

// 튜플 구조체
struct Pair(i32, f32);

// 2개의 필드가 있는 구조체
struct Point {
    x: f32,
    y: f32,
}

// 구조체는 다른 구조체를 필드로 사용할 수 있습니다.
struct Rectangle {    
    // retangle 구조체는 왼쪽 상단과 오른쪽 하단의 좌표로 지정할 수 있습니다.
    top_left: Point,
    bottom_right: Point,
}

fn main() {
    // 각 필드를 초기화 하면서 구조체 생성 (이름을 생략함)
    let name = String::from("Peter");
    let age = 27;
    let peter = Person { name, age };

    // 구조체 디버그 프린트
    println!("{:?}", peter);

    // `Point` 구조체 생성
    let point: Point = Point { x: 10.3, y: 0.4 };

    // point 필드에 접근
    println!("point coordinates: ({}, {})", point.x, point.y);

    // 구조체 업데이트 문법을 사용하여, 다른 구조체의 필드를 사용하여 새로운 point 생성
    let bottom_right = Point { x: 5.2, ..point };

    // `point`의 필드를 사용하기 때문에, `bottom_right.y` 는  `point.y` 동일합니다. 
    println!("second point: ({}, {})", bottom_right.x, bottom_right.y);

    // `let` 바인딩을 이용한 해체 (구조체 필드로 나누기)
    let Point { x: left_edge, y: top_edge } = point;

    let _rectangle = Rectangle {
        // struct 생성은 표현식입니다.
        top_left: Point { x: left_edge, y: top_edge },
        bottom_right: bottom_right,
    };

    // 유닛 구조체 생성
    let _unit = Unit;

    // 튜플 구조체 생성
    let pair = Pair(1, 0.1);

    // 튜플 구조체 필드 접근
    println!("pair contains {:?} and {:?}", pair.0, pair.1);

    // 튜플 구조체 해체
    let Pair(integer, decimal) = pair;

    println!("pair contains {:?} and {:?}", integer, decimal);
}
```

### 실습

1. `Rectangle`의 넓이를 계산하는 `rect_area` 함수를 만드세요.
    (중첩된 해체를 사용해보세요.)
2. `Point` 와 `f32`를 인수로 갖는 `square` 함수를 만들어, point의 넓이와 높이가 `f32`와 
   일치하고 왼쪽 상단이 `Point` 인 `Rectangle` 을 리턴하세요.

### See also

[`attributes`][attributes], and [destructuring][destructuring]

[attributes]: ../attribute.md
[c_struct]: https://en.wikipedia.org/wiki/Struct_(C_programming_language)
[destructuring]: ../flow_control/match/destructuring.md
