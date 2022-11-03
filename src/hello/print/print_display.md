# Display

`fmt::Debug` 트레이트는 컴팩트하지도 않고, 깔끔해 보이지도 않습니다. 그래서 보통 출력 형태를 사용자   
정의로 변경하는 것이 좋습니다. 사용자 정의 변경하는 것은 [`fmt::Display`][fmt] 트레이트를   
구현해야 하고, 그러고 나면 `{}` 마커를 사용할 수 있게 됩니다.  
구현하는 방법은 아래처럼 하면 됩니다.

```rust
// `use` 키워드로 `fmt` 모듈을 사용할 수 있게 임포트 합니다.
use std::fmt;

// `fmt::Display` 를 구현할 구조체를 정의합니다. This is
// `Structure` 는 튜플 구조체이고, `i32`값을 담을 수 있습니다.
struct Structure(i32);

// `{}` 마커를 사용하기 위해서는 `fmt::Display` 트레이트가 타입에 맞게 구현되어야 합니다.
impl fmt::Display for Structure {    
    //`fmt::Display` 트레이트는 아래처럼 `fmt` 함수의 정확한 시그니처를 요구합니다.
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {        
        // 첫번째 요소를 제공된 출력 스트림 `f` 에 쓰기를 합니다. 
        // `fmt::Result`을 리턴해서 성공인지 실패인지 알려줍니다.
        // `write!` 는 `println!` 와 거의 비슷한 문법을 사용하는 것에 주목하세요.
        write!(f, "{}", self.0)
    }
}
```

`fmt::Display` 트레이트는 `fmt::Debug` 트레이트보다 깔끔할 수는 있지만
`std` 라이브러리 대한 문제가 있습니다. 모호한 타입은 어떻게 보여져야 할까요?
예컨대, `std` 라이브러리가 모든 `Vec<T>`에 대해 단 하나의 스타일만 구현한다면,
어떤 스타일이 되어야 할까요? 다음 둘 중 하나가 될까요?

* `Vec<path>`: `/:/etc:/home/username:/bin` (split on `:`)
* `Vec<number>`: `1,2,3` (split on `,`)

아닙니다. 모든 타입에 대해 이상적인 스타일은 없고, `std` 라이브러리는 어떤 하나의 스타일을 
가정하지 않습니다. 
`Vec<T>` 와 다른 제네릭 컨테이너들은 `fmt::Display`트레이트를 구현하지 않습니다.
일반적인 경우에는 `fmt::Debug` 트레이트를 사용해야 합니다.

새로운 컨테이너가 제네릭이 아닌 경우에는 `fmt::Display`를 구현될 수 있어 문제가 되진 않습니다.

```rust,editable
use std::fmt; // 임포트 `fmt`

// 다음 구조체는 두 개의 숫자를 가집니다. 
// `Display` 트레이트와는 다르게 `Debug` 트레이트는 상속됩니다.
#[derive(Debug)]
struct MinMax(i64, i64);

// `MinMax` 구조체에 대한 `Display` 트레이트 구현.
impl fmt::Display for MinMax {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // 각 숫자를 참조하기 위해서는 `self.number`를 사용하세요.        
        write!(f, "({}, {})", self.0, self.1)
    }
}

// 비교를 위해 이름이 있는 필드들이 있는 구조체를 정의합니다.
#[derive(Debug)]
struct Point2D {
    x: f64,
    y: f64,
}

// 유사하게 `Point2D`구조체를 대한 `Display` 트레이트를 구현합니다.
impl fmt::Display for Point2D {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // `x` 와 `y`만 표시되도록 정의합니다.
        write!(f, "x: {}, y: {}", self.x, self.y)
    }
}

fn main() {
    let minmax = MinMax(0, 14);

    println!("Compare structures:");
    println!("Display: {}", minmax);
    println!("Debug: {:?}", minmax);

    let big_range =   MinMax(-300, 300);
    let small_range = MinMax(-3, 3);

    println!("The big range is {big} and the small is {small}",
             small = small_range,
             big = big_range);

    let point = Point2D { x: 3.3, y: 7.2 };

    println!("Compare points:");
    println!("Display: {}", point);
    println!("Debug: {:?}", point);

    // `Debug`와 `Display`가 구현되었지만, `{:b}` 는 `fmt::Binary` 의 구현이 
    // 필요하기 때문에 에러입니다. (주석을 제거하면) 동작하지 않을 것 입니다.
    // println!("What does Point2D look like in binary: {:b}?", point);
}
```

`fmt::Display` 는 구현되었지만, `fmt::Binary` 가 구현되지 않아서 사용할 수 업습니다.
`std::fmt` 에는 이런 [`트레이트`][traits]가 많이 있으며, 각각의 구현을 필요로 합니다.
더 자세한 내용은 [`std::fmt`][fmt] 에 있습니다.

### 활동

위의 예제의 출력 결과를 확인한 후에, `Point2D` 구조체를 가이드로 해서 `Complex` 구조체를 
이 예제에 추가해 보세요. 같은 방법으로 출력된다면, 결과는 다음처럼 나와야 합니다.

```txt
Display: 3.3 + 7.2i
Debug: Complex { real: 3.3, imag: 7.2 }
```

### See also:

[`derive`][derive], [`std::fmt`][fmt], [`macros`][macros], [`struct`][structs],
[`trait`][traits], and [`use`][use]

[derive]: ../../trait/derive.md
[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../../macros.md
[structs]: ../../custom_types/structs.md
[traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[use]: ../../mod/use.md
