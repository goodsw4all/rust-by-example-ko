# 리터럴<sup>Literals</sup>과 연산자

정수 `1`, 부동소수점 `1.2`, 문자 `'a'`, 문자열 `"abc"`, 불리언 `true`
과 유닛타입 `()`은 리터럴로 표현할 수 있습니다.

정수<sup>Integers</sup>는 16진수, 8진수 혹은 2진수로 표기할 수 있습니다.
각각 `0x`, `0o` `0b`  접두사를 이용하면 됩니다.

가독성을 위해 숫자 리터럴에는  **_**<sup>Underscores</sup>를 사용할 수 있습니다. 
예. `1_000` 은 `1000`와 같고, `0.000_001`은 `0.000001`과 동일합니다.

사용하려는 리터럴이 컴파일러에게 어떤 종류인지 알려주는 것이 필요합니다. 
일단 `u32` 접미사를 사용해 부호없는 32비트 정수를, `i32` 접미사를 사용해 부호있는 32비트
정수를 표현할 때 사용합니다.

[Rust 에서][rust op-prec] 사용할 수 있는 연산자들과 연산자 우선순위는 
[C언어 계열의 언어들][op-prec]과 유사합니다.

```rust,editable
fn main() {
    // 정수 더하기
    println!("1 + 2 = {}", 1u32 + 2);

    // 정수 빼기
    println!("1 - 2 = {}", 1i32 - 2);
    // TODO ^ 자료형의 중요성을 알아보기 위해 `1i32` 를 `1u32`으로 변경해보세요.

    // 불리언 논리 연산
    println!("true AND false is {}", true && false);
    println!("true OR false is {}", true || false);
    println!("NOT true is {}", !true);

    // 비트 연산
    println!("0011 AND 0101 is {:04b}", 0b0011u32 & 0b0101);
    println!("0011 OR 0101 is {:04b}", 0b0011u32 | 0b0101);
    println!("0011 XOR 0101 is {:04b}", 0b0011u32 ^ 0b0101);
    println!("1 << 5 is {}", 1u32 << 5);
    println!("0x80 >> 2 is 0x{:x}", 0x80u32 >> 2);

    // 가독성을 위한 언더스코어 사용!
    println!("One million is written as {}", 1_000_000u32);
}
```

[rust op-prec]: https://doc.rust-lang.org/reference/expressions.html#expression-precedence
[op-prec]: https://en.wikipedia.org/wiki/Operator_precedence#Programming_languages
