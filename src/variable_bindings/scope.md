# 범위<sup>Scope</sup> 와 쉐도잉<sup>Shadowing</sup>

Variable bindings have a scope, and are constrained to live in a *block*. A
block is a collection of statements enclosed by braces `{}`. 
변수 바인딩은 범위를 가지며, **블록 block** 안에서 유효하도록 제한 됩니다. 
블록은 statement 들을 `{}`으로 둘러쌓은 것을 말합니다.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // 이 바인딩은 main함수 안에서만 유효합니다.
    let long_lived_binding = 1;

    // 다음은 하나의 블록이며 main 함수보다 더 작은 범위 입니다.
    {
        // 다음 바인딩은 이 블록에서만 유효합니다.
        let short_lived_binding = 2;

        println!("inner short: {}", short_lived_binding);
    }
    // 블록 끝

    // `short_lived_binding`은 더 이상 범주에 속하지 않으므로 Error!
    println!("outer short: {}", short_lived_binding);
    // FIXME ^ 위의 라인를 주석 처리하세요.

    println!("outer long: {}", long_lived_binding);
}
```
또, [변수 쉐도잉][variable-shadow]이 허용됩니다.
```rust,editable,ignore,mdbook-runnable
fn main() {
    let shadowed_binding = 1;

    {
        println!("before being shadowed: {}", shadowed_binding);

        // 이 바인딩은 블록 범위 밖에 있는 변수를 *쉐도잉* 합니다.
        let shadowed_binding = "abc";

        println!("shadowed in inner block: {}", shadowed_binding);
    }
    println!("outside inner block: {}", shadowed_binding);

    // 이 바인딩은 위의 변수를 *쉐도잉* 합니다.
    let shadowed_binding = 2;
    println!("shadowed in outer block: {}", shadowed_binding);
}
```
[variable-shadow]: https://en.wikipedia.org/wiki/Variable_shadowing
