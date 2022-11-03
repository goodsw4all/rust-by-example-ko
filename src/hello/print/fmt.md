# 서식 <sup>Formatting</sup>

 **format string** 을 통해서 서식을 어떻게 지정하는 지 살펴보았습니다.

* `format!("{}", foo)` -> `"3735928559"`
* `format!("0x{:X}", foo)` ->
  [`"0xDEADBEEF"`][deadbeef]
* `format!("0o{:o}", foo)` -> `"0o33653337357"`

같은 변수 (`foo`) 는 어떤 **인수 타입**이냐에 따라 다른 서식이 될 수 있습니다.
`X` vs `o` vs **unspecified**.

서식화하는 기능은 트레이트를 통해 구현되고, 각 인수에 대해 하나의 트레이트가 존재합니다.
가장 흔한 서식 트레이트는 `Display` 이고, 인수 타입이 정해지지 않은 경우를 처리합니다. 예 `{}`

```rust,editable
use std::fmt::{self, Formatter, Display};

struct City {
    name: &'static str,
    // 위도
    lat: f32,
    // 경도
    lon: f32,
}

impl Display for City {
    // 다음 메소드는 `f` 버퍼에 서식화된 string 을 write 해야 합니다.
    fn fmt(&self, f: &mut Formatter) -> fmt::Result {
        let lat_c = if self.lat >= 0.0 { 'N' } else { 'S' };
        let lon_c = if self.lon >= 0.0 { 'E' } else { 'W' };

        // `write!` 는 `format!` 과 유사하지만, string 을 buffer(첫째 인수)에 write 합니다.        
        write!(f, "{}: {:.3}°{} {:.3}°{}",
               self.name, self.lat.abs(), lat_c, self.lon.abs(), lon_c)
    }
}

#[derive(Debug)]
struct Color {
    red: u8,
    green: u8,
    blue: u8,
}

fn main() {
    for city in [
        City { name: "Dublin", lat: 53.347778, lon: -6.259722 },
        City { name: "Oslo", lat: 59.95, lon: 10.75 },
        City { name: "Vancouver", lat: 49.25, lon: -123.1 },
    ].iter() {
        println!("{}", *city);
    }
    for color in [
        Color { red: 128, green: 255, blue: 90 },
        Color { red: 0, green: 3, blue: 254 },
        Color { red: 0, green: 0, blue: 0 },
    ].iter() {
        // Switch this to use {} once you've added an implementation
        // for fmt::Display.
        println!("{:?}", *color);
    }
}
```

[모든 서식 트레이트 리스트][fmt_traits]를 볼 수 있고, 각 인수타입들은  
[`std::fmt`][fmt] 문서에서 볼 수 있습니다.

### 실습
`Color` 구조체 대해 `fmt::Display` 트레이트를 구현해서 아래처럼
출력되도로 해보세요.

```text
RGB (128, 255, 90) 0x80FF5A
RGB (0, 3, 254) 0x0003FE
RGB (0, 0, 0) 0x000000
```

잘 안 될 경우를 위한 힌트 2개:
 * [각 칼러에 대해 한 번이상 나열해야 할 수 있습니다.][named_parameters],
 * [width 가 2인 경우에 0을 패딩할 수 있습니다.][fmt_width] with `:0>2`.

### 참고:

[`std::fmt`][fmt]

[named_parameters]: https://doc.rust-lang.org/std/fmt/#named-parameters
[deadbeef]: https://en.wikipedia.org/wiki/Deadbeef#Magic_debug_values
[fmt]: https://doc.rust-lang.org/std/fmt/
[fmt_traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[fmt_width]: https://doc.rust-lang.org/std/fmt/#width
