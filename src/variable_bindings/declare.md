# 선언 먼저 하기

변수를 먼저 선언하고 나중에 초기화 하는 것이 가능합니다. 그렇지만, 이런 방식은 초기화 되지 않은 변수를 사용하게 할 수 있어 거의 사용하지 않습니다.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // 변수 바인딩 선언
    let a_binding;

    {
        let x = 2;

        // 선언한 바인딩 초기화 
        a_binding = x * x;
    }

    println!("a binding: {}", a_binding);

    let another_binding;

    // 초기화 되지 않은 사용으로 Error!
    println!("another binding: {}", another_binding);
    // FIXME ^ 주석 처리 하세요.

    another_binding = 1;

    println!("another binding: {}", another_binding);
}
```

undefined 결과를 만들 수 있기 때문에, 컴파일러가 초기화 되지 않은 변수의 사용을 금지합니다.
