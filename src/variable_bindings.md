# 변수 바인딩

Rust 는 정적 타이핑을 통해 타입 안정성을 제공합니다. 변수 바인딩은 변수 선언시에 타입 어노테이션
으로 할 수 있습니다. 하지만, 대부분의 경우에 컴파일러는 문맥에 따라 변수의 타입을 유추할 수 있어서
타입 어노테이션해야하는 부담을 많이 줄여 줍니다.


리터럴 같은 값<sup>value</sup>은 `let` 키워드로 변수에 바인딩합니다.

```rust,editable
fn main() {
    let an_integer = 1u32;
    let a_boolean = true;
    let unit = ();

    // `an_integer`를 `copied_integer`으로 복사
    // 
    let copied_integer = an_integer;

    println!("An integer: {:?}", copied_integer);
    println!("A boolean: {:?}", a_boolean);
    println!("Meet the unit value: {:?}", unit);

    // 컴파일러는 사용하지 않는 변수 바인딩에 대해서 경고를 주는 데, 변수 이름 앞에
    // _ 를 붙여주면, 이런 경고를 생략합니다.
    let _unused_variable = 3u32;

    let noisy_unused_variable = 2u32;
    // FIXME ^ _ 를 변수 이름 앞에 붙여서 경고를 숨겨보세요.    
    // 브라우저에서는 경고가 보이지 않을 수 있으니, 주의하세요.
}
```
