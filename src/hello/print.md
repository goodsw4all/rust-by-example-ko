# 서식있는 프린트 <sup>Formatted print</sup>

프린팅은 [`std::fmt`][fmt] 모듈에 정의되어 있는 일련의 [`매크로`][macros] 가 처리합니다.

* `format!`: 서식있는 텍스트를 [`String`][string] 구조체로 만들어 반환합니다.
* `print!`: `format!` 과 동일하지만, 텍스트를 콘솔(io::stdout)로 출력합니다. 
* `println!`: `print!` 와 동일하고, 새로운 줄을 추가합니다.
* `eprint!`: `print!` 와 동일하지만, 텍스트를 표준에러 (io::stderr)로 출력합니다.
* `eprintln!`: `eprint!` 와 동일하고, 새로운 줄을 추가합니다.

위의 모든 매크로가 같은 방식으로 텍스트를 파싱합니다. 또한 Rust는 서식에 오류가 없는지 컴파일 타임에 검사합니다.

```rust,editable,ignore,mdbook-runnable
fn main() {    
    // 일반적으로 `{}`는 인수가 스트링화 되어 자동으로 변경됩니다.
    println!("{} days", 31);

    // 인수의 순서를 지정할 수 있습니다. `{}` 에 정수를 넣어 몇번째 인수를 사용할지 결정합니다.
    // 인수 순서는 서식있는 스트링에 바로 다음부터 0에서 시작합니다.      
    println!("{0}, this is {1}. {1}, this is {0}", "Alice", "Bob");

    // 인수의 이름을 넣을 수도 있습니다..
    println!("{subject} {verb} {object}",
             object="the lazy dog",
             subject="the quick brown fox",
             verb="jumps over");

    // 서식 문자를 이용해 다른 서식을 적용할 수 있습니다.
    // `:`.
    println!("Base 10:               {}",   69420); //69420
    println!("Base 2 (binary):       {:b}", 69420); //10000111100101100
    println!("Base 8 (octal):        {:o}", 69420); //207454
    println!("Base 16 (hexadecimal): {:x}", 69420); //10f2c
    println!("Base 16 (hexadecimal): {:X}", 69420); //10F2C


    // 텍스트를 지정한 너비로 오른쪽 정렬할 수 있습니다. This will
    // 다음의 출력결과는 output "    1" 입니다. 전체 너비 5에 4개의 스페이스와 "1" 입니다.
    println!("{number:>5}", number=1);

    // 0을 패딩할 수 있습니다.
    // 그리고 부등호 방향을 뒤집어 왼족정렬 합니다. 출력은 "10000"이 됩니다.
    println!("{number:0<5}", number=1);

    // 인수 이름에 '$'를 붙여서 서식 기호에 사용할 수 있습니다.
    println!("{number:0>width$}", number=1, width=5);

    // Rust는 사용한 인수의 개수가 맞는지 확인합니다.
    println!("My name is {0}, {1} {0}", "Bond");
    // FIXME ^ 부족한 인수를 추가하세요: "James"

    // fmt::Display 트레이트를 구현하는 자료형들만 `{}`에 사용할 수 있습니다. User-
    // 사용자 정의 자료형은 fmt::Display 를 디폴트로 구현하지 않습니다.

    #[allow(dead_code)]
    struct Structure(i32);

    // 다음은 `Structure`가  fmt::Display를 구현하지 않았기 때문에 컴파일 되지 않습니다.    
    //println!("This struct `{}` won't print...", Structure(3));
    // TODO ^ 주석을 지워 보세요.

    // Rust 1.58 이상에서는, 주위의 변수들을 인수로 사용할 수 있습니다.
    // 바로 위에서 본것처럼, 출력결과는 "    1".
    // 4개의 스페이스와 "1" 입니다..
    let number: f64 = 1.0;
    let width: usize = 5;
    println!("{number:>width$}");
}
```
[`std::fmt`][fmt] 모듈은 텍스트가 보여지는 방식을 정하는 다양한 [`트레이트`][traits]를 포함하고 있습니다.   
아래에 두 가지 중요한 기본 형태가 있습니다.

* `fmt::Debug`: `{:?}` 마커를 사용합니다. 디버깅용으로 텍스트 형식을 지정합니다.
* `fmt::Display`: `{}` 마커를 사용합니다. 텍스트 형식을 보다 우아하고, 사용자 친화적으로 지정합니다.

std 라이브러는 자료형에 대해 `fmt::Display` 트레이트를 제공하므로, 예제에서 사용할 수 있었습니다.   
사용자 정의 자료형에 대해서는 몇가지 단계가 더 필요합니다.

`fmt::Display`트레이트를 구현하면, [`String`][string] 타입으로 [`변환`][convert] 변환해주는   
[`ToString`]트레이트가 자동으로 구현됩니다.

### 실습

 * FIXME 부분을 수정해서 에러없이 예제를 실행해보세요.   
 * TODO 부분의 `Structure` 구조체가 있는 줄의 주석을 지워보세요.
 * 자리수를 제어해서 `Pi is roughly 3.142`를 출력하는 매크로를 추가해보세요. 
   pi 변수는 `let pi = 3.141592`을 사용합니다. 
   (힌트: [`std::fmt`][fmt] 문서에서 자리수를 세팅하는 것을 찾아보세요)

### 참고:

[`std::fmt`][fmt], [`macros`][macros], [`struct`][structs],
and [`traits`][traits]

[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../macros.md
[string]: ../std/str.md
[structs]: ../custom_types/structs.md
[traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[`ToString`]: https://doc.rust-lang.org/std/string/trait.ToString.html
[convert]: ../conversion/string.md
