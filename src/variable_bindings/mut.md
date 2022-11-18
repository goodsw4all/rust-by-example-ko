# 가변성<sup>Mutability</sup>

Variable bindings are immutable by default, but this can be overridden using
the `mut` modifier.
변수 바인딩은 불변<sup>immutable</sup> 속성을 디폴트로 합니다. 
하지만, `mut` 키워드를 사용하면 이 속성은 변경될 수 있습니다.

```rust,editable,ignore,mdbook-runnable
fn main() {
    let _immutable_binding = 1;
    let mut mutable_binding = 1;

    println!("Before mutation: {}", mutable_binding);

    // Ok
    mutable_binding += 1;

    println!("After mutation: {}", mutable_binding);

    // Error!
    _immutable_binding += 1;
    // FIXME ^ 주석처리하세요.
}
```

컴파일러가 가변성 관련 에러에 대한 자세한 진단을 보여줄 것 입니다.
