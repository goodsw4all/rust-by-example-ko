# Testcase: List

각 요소들이 순차적으로 처리해야 하는 구조체의 `fmt::Display` 트레이트를 구현하는 것은 까다롭습니다.
각각의 `write!` 매크로는 `fmt::Result`를 리턴합니다.
이를 제대로 처리하기 위해서는 각 result를 처리하는 것이 필요합니다.
Rust는 이를 위해 `?` 연산자를 제공합니다.

`write!` 매크로에 대해 `?`를 사용하는 것은 아래와 같습니다.

```rust,ignore
// `write!`가 에러를 리턴하는지 시도합니다. 에러라면 그 에러를 리턴합니다.
// 에러가 아니라면 계속 실행합니다.
write!(f, "{}", value)?;
```

`?`를 사용할 수 있으니, `Vec` 에 대한 `fmt::Display` 를 구현하는 것은 복잡하지 않습니다.

```rust,editable
use std::fmt; // `fmt` 모듈을 임포트합니다.

// `Vec`를 소유하는 `List` 구조체를 정의합니다.
struct List(Vec<i32>);

impl fmt::Display for List {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {        
        // 튜플 인덱싱을 이용해 값을 가져와 `vec`의 레퍼런스를 생성합니다.
        let vec = &self.0;

        write!(f, "[")?;

        // `vec`에서 `v`를 이터레이트 하면서, 
        // `count` 변수에 반복 카운트를 열거합니다.
        for (count, v) in vec.iter().enumerate() {
            // 첫번째 항목을 제외한 모든 항목에 컴마를 붙입니다.            
            // 에러시 리턴할 수 있게 ? 연산자를 사용합니다.
            if count != 0 { write!(f, ", ")?; }
            write!(f, "{}", v)?;
        }
        
        // 열었던 괄호를 닫고 fmt::Result 를 리턴합니다.
        write!(f, "]")
    }
}

fn main() {
    let v = List(vec![1, 2, 3]);
    println!("{}", v);
}
```

### 실습

벡터의 각 항목들의 인데스가 출력되도록 프로그램을 변경해 보세요. 새로운 출력은 다음과 같습니다.

```rust,ignore
[0: 1, 1: 2, 2: 3]
```

### 참고:

[`for`][for], [`ref`][ref], [`Result`][result], [`struct`][struct],
[`?`][q_mark], and [`vec!`][vec]

[for]: ../../../flow_control/for.md
[result]: ../../../std/result.md
[ref]: ../../../scope/borrow/ref.md
[struct]: ../../../custom_types/structs.md
[q_mark]: ../../../std/result/question_mark.md
[vec]: ../../../std/vec.md
