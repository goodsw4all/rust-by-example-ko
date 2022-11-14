# 사용

`use` 선언을 사용하면, 수동 범위 지정을 할 필요 없습니다.

```rust,editable
// 사용하지 않는 코드에 대한 경고를 숨기는 속성
#![allow(dead_code)]

enum Status {
    Rich,
    Poor,
}

enum Work {
    Civilian,
    Soldier,
}

fn main() {    
    // `use`를 명시적으로 각각의 이름에 사용해서 수동 범위지정 없이 사용가능하게 합니다.
    use crate::Status::{Poor, Rich};
    // 자동으로 `Work`의 모든 이름에 `use` 를 사용합니다.
    use crate::Work::*;

    // `Status::Poor` 와 같음.
    let status = Poor;
    // `Work::Civilian`와 같음.
    let work = Civilian;

    match status {        
        // 위에서 명시적으로 `use`를 썼기 때문에 범위 지정이 없음에 주의하세요.
        Rich => println!("The rich have lots of money!"),
        Poor => println!("The poor have no money..."),
    }

    match work {
        // 다시 한번, 범위 지정이 없음에 주의하세요.
        Civilian => println!("Civilians work!"),
        Soldier  => println!("Soldiers fight!"),
    }
}
```

### 참고:

[`match`][match], [`use`][use] 

[use]: ../../mod/use.md
[match]: ../../flow_control/match.md
