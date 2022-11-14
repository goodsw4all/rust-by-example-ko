# C언어 스타일로 사용 <sup>C-like</sup>

`enum`은 C언어에서 사용하듯이 사용할 수 있습니다.

```rust,editable
// 사용하지 않는 코드에 대한 경고를 숨기는 속성
#![allow(dead_code)]

// 명시적으로 값을 주지 않은 enum (0 부터 시작)
enum Number {
    Zero,
    One,
    Two,
}

// 명시적으로 값을 준 enum 
enum Color {
    Red = 0xff0000,
    Green = 0x00ff00,
    Blue = 0x0000ff,
}

fn main() {
    // `enums`을 정수로 변환할 수 있습니다.
    println!("zero is {}", Number::Zero as i32);
    println!("one is {}", Number::One as i32);

    println!("roses are #{:06x}", Color::Red as i32);
    println!("violets are #{:06x}", Color::Blue as i32);
}
```

### 참고:

[casting][cast]

[cast]: ../../types/cast.md
