# Debug

`std::fmt` 모둘의 서식화하는 `traits` 를 사용하기 위해서는 프린트할 수 있게 해주는 구현이 필요합니다.
`std` 라이브러리에 있는 자료형에 대해서만 `traits`를 자동구현 합니다. 다른 모든 자료형들은 *꼭*   
직접 구현해야 합니다.

`fmt::Debug` `trait`는 매우 직관적이다.  *모든* 자료형은 `fmt::Debug` 의 구현을   
`상속`<sup>derive</sup> (자동 생성) 받을 수 있습니다.   
`fmt::Display` 은 해당되지 않고, 직접 구현해야 합니다.

```rust
// 다음 구조체는 `fmt::Display` 이나 with `fmt::Debug` 으로
// 프린트 할 수 없습니다.
struct UnPrintable(i32);

// 아래처럼 `derive` 속성을 주면 `struct`를 `fmt::Debug`로 프린트할 수 있게 하는 구현을    
// 자동으로 만들어 냅니다.
#[derive(Debug)]
struct DebugPrintable(i32);
```

`std` 라이브러리의 모든 타입은 자동으로 `{:?}`을 사용해 프린트할 수 있습니다.

```rust,editable
// `Structure`에 `fmt::Debug` 구현을 상속받습니다. 
// `Structure` 에는 하나의 `i32`를 가지고 있습니다.
#[derive(Debug)]
struct Structure(i32);

// `Deep` 구조체에 `Structure` 구조체를 넣습니다.
// `derive`로 프린트 할 수 있게 만듭니다.
#[derive(Debug)]
struct Deep(Structure);

fn main() {
    // `{:?}`로 프린트하는 것은 `{}` 와 비슷합니다.
    println!("{:?} months in a year.", 12);
    println!("{1:?} {0:?} is the {actor:?} name.",
             "Slater",
             "Christian",
             actor="actor's");

    // `Structure` 구조체는 프린트 할 수 있습니다.
    println!("Now {:?} will print!", Structure(3));
    
    // `derive` 속성의 문제는 결과가 어떻게 보일지 제어할 수 없다는 것 입니다.
    // 단지 `7` 만 보이게 하고 싶다면요?
    println!("Now {:?} will print!", Deep(Structure(7)));
}
```

`fmt::Debug` 트레이트는 프린트 할 수 있게 해주지만, 우아함을 좀 희생해야 합니다.   
Rust 는 `{:#?}`을 사용해서 "pretty printing"을 제공합니다.

```rust,editable
#[derive(Debug)]
struct Person<'a> {
    name: &'a str,
    age: u8
}

fn main() {
    let name = "Peter";
    let age = 27;
    let peter = Person { name, age };

    // Pretty print
    println!("{:#?}", peter);
}
```

출력되는 것을 제어하고 싶다면 `fmt::Display`를 구현하면 됩니다.

### 참고:

[`attributes`][attributes], [`derive`][derive], [`std::fmt`][fmt],
and [`struct`][structs]

[attributes]: https://doc.rust-lang.org/reference/attributes.html
[derive]: ../../trait/derive.md
[fmt]: https://doc.rust-lang.org/std/fmt/
[structs]: ../../custom_types/structs.md

