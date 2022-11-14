# 열거형 <sup>Enum</sup>

`enum` 키워드는 여러 유형 중 한가지가 될 수 있는 자료형을 정의하게 해줍니다.
`struct` 에서 유효한 것은  `enum` 에서도 유효합니다.

```rust,editable
// 웹 이벤트를 분류하는 `enum` 만듭니다.
// 각 필드의 이름과 자료형 정보를 어떻게 명시하는 지 주의해서 보세요.
// `PageLoad != PageUnload` 와 `KeyPress(char) != Paste(String)`는
// 서로 다르고 독립적 입니다.
enum WebEvent {
    // 유닛 스타일의 `enum`
    PageLoad,
    PageUnload,
    // 튜플 구조체 스타일,
    KeyPress(char),
    Paste(String),
    // C언어 구조체 스타일
    Click { x: i64, y: i64 },
}

// `WebEvent` enum 을 인수로 갖고 리턴값이 없는 함수
fn inspect(event: WebEvent) {
    match event {
        WebEvent::PageLoad => println!("page loaded"),
        WebEvent::PageUnload => println!("page unloaded"),        
        // `enum` 자료형 안에 있는 값을  `c`로 추출
        WebEvent::KeyPress(c) => println!("pressed '{}'.", c),
        WebEvent::Paste(s) => println!("pasted \"{}\".", s),        
        // `Click` 자료형의 필드들을 `x`와 `y` 로 추출
        WebEvent::Click { x, y } => {
            println!("clicked at x={}, y={}.", x, y);
        },
    }
}

fn main() {
    let pressed = WebEvent::KeyPress('x');
    // `to_owned()`함수는 슬라이스에서 소유권 있는 `String`을 생성합니다.
    let pasted  = WebEvent::Paste("my text".to_owned());
    let click   = WebEvent::Click { x: 20, y: 80 };
    let load    = WebEvent::PageLoad;
    let unload  = WebEvent::PageUnload;

    inspect(pressed);
    inspect(pasted);
    inspect(click);
    inspect(load);
    inspect(unload);
}

```

## 자료형 별명 <sup>Type aliases</sup>

자료형에 별명을 사용하면, 각 enum의 유형을 별명으로 참조할 수 있습니다.
enum의 이름이 너무 길거나 너무 일반적이어서 이름을 다시 만들고 싶을 때 유용합니다.

```rust,editable
enum VeryVerboseEnumOfThingsToDoWithNumbers {
    Add,
    Subtract,
}

// 자료형 별명을 만듭니다.
type Operations = VeryVerboseEnumOfThingsToDoWithNumbers;

fn main() {    
    // 길고 불편한 이름이 아닌 별명으로 각 유형을 참조할 수 있습니다.
    let x = Operations::Add;
}
```

자료형 별명이 가장 흔하게 사용되는 곳은 `impl` 코드 블록에서 사용하는 `Self` 별명입니다.

```rust,editable
enum VeryVerboseEnumOfThingsToDoWithNumbers {
    Add,
    Subtract,
}

impl VeryVerboseEnumOfThingsToDoWithNumbers {
    fn run(&self, x: i32, y: i32) -> i32 {
        match self {
            Self::Add => x + y,
            Self::Subtract => x - y,
        }
    }
}
```

enum과 자료형 별명에 대해서 더 알고 싶다면, 이 기능이 Rust에서 안정화 되었을 때의 [안정화 보고서][aliasreport]를 읽어 보실 수 있습니다. 


### 참고:

[`match`][match], [`fn`][fn], [`String`][str], ["Type alias enum variants" RFC][type_alias_rfc]

[c_struct]: https://en.wikipedia.org/wiki/Struct_(C_programming_language)
[match]: ../flow_control/match.md
[fn]: ../fn.md
[str]: ../std/str.md
[aliasreport]: https://github.com/rust-lang/rust/pull/61682/#issuecomment-502472847
[type_alias_rfc]: https://rust-lang.github.io/rfcs/2338-type-alias-enum-variants.html
