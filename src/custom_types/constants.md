# 상수 <sup>constants</sup>

Rust에는 전역범위를 포함한 어떤 범위에서도 선언할 수 있는 2가지 타입의 상수가 있습니다.
둘다 명시적으로 타입 어노테이션을 해야 합니다.

* `const`: 변경 불가능한 값 (대부분의 경우).
* `static`: `변경 가능`하고 [`'static`][static] 라이프 타임을 갖습니다.
  static 라이프타임 추론되기 때문에 명시적으로 선언할 필요가 없습니다.

  변경가능한 static 변수를 접근하거나 수정하는 것은 [`unsafe`][unsafe] 입니다.

```rust,editable,ignore,mdbook-runnable
// 전역변수는 가장 바깥에 선언 됩니다.
static LANGUAGE: &str = "Rust";
const THRESHOLD: i32 = 10;

fn is_big(n: i32) -> bool {
    // 함수에서 상수 접근하기
    n > THRESHOLD
}

fn main() {
    let n = 16;
    
    // 메인 쓰레드에서 상수 접근하기
    println!("This is {}", LANGUAGE);
    println!("The threshold is {}", THRESHOLD);
    println!("{} is {}", n, if is_big(n) { "big" } else { "small" });

    // 에러! `const` 변수를 수정할 수 없습니다.
    THRESHOLD = 5;
    // FIXME ^ 주석처리 해보세요.
}
```

### 참고:

[The `const`/`static` RFC](
https://github.com/rust-lang/rfcs/blob/master/text/0246-const-vs-static.md),
[`'static` lifetime][static]

[static]: ../scope/lifetime/static_lifetime.md
[unsafe]: ../unsafe.md
