# 원시자료형<sup>Primitives</sup>
러스트는 다양한 원시자료형을 제공합니다. 원시자료형은 다음과 같은 자료형을 포함합니다.

### 스칼라<sup>Scalar</sup> 자료형
* 부호있는 정수: `i8`, `i16`, `i32`, `i64`, `i128` and `isize` (pointer size)
* 부호없는 정수: `u8`, `u16`, `u32`, `u64`, `u128` and `usize` (pointer
  size)
* 부동소수점: `f32`, `f64`
* 문자 `char`: 유니코드 스칼라 값 like `'a'`, `'α'` and `'∞'` (각 문자 4 bytes)
* 부울 `bool`: `true` 이거나 `false`
* 유닛 자료형 `()`: 비어있는 튜플:`()`

유닛 자료형은 튜플이긴 하지만, 값을 가지지 않으므로 복합자료형으로 고려하지 않습니다.

### 복합<sup>Compound</sup> 자료형

* 배열 표현 `[1, 2, 3]`
* 튜플 표현 `(1, true)`

변수에는 항상 자료형을 표기합니다. 숫자들은 **접미사**<sup>suffix</sup>를 붙이거나
기본자료형으로 사용됩니다. 정수는 기본값이 `i32`이고, 부동소수점의 기본값은 `f64`입니다.
러스트는 문맥에서 자료형을 추론할 수 있습니다.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // 변수에는 자료형을 표기합니다.
    let logical: bool = true;

    let a_float: f64 = 1.0;  // 일반적인 자료형 표기
    let an_integer   = 5i32; // 접미사로 자료형 표기

    // 기본 자료형 사용
    let default_float   = 3.0; // `f64`
    let default_integer = 7;   // `i32`
    
    // 문맥에서 자료형을 유추할 수 있습니다.
    let mut inferred_type = 12; // 다음 줄에서 i64 로 추론합니다.
    inferred_type = 4294967296i64;
    
    // 가변 변수는 값이 변경될 수 있습니다.
    let mut mutable = 12; // 가변 `i32`
    mutable = 21;
    
    // 에러! 자료형은 바꿀 수 없습니다.
    mutable = true;
    
    // 쉐도잉으로 변수를 덮어 쓸 수 있습니다.
    let mutable = true;
}
```

### 참고:

[the `std` library][std], [`mut`][mut], [`inference`][inference], and [`shadowing`][shadowing]

[std]: https://doc.rust-lang.org/std/
[mut]: variable_bindings/mut.md
[inference]: types/inference.md
[shadowing]: variable_bindings/scope.md
