# 테스트 케이스: linked-list

linked-list 를  `enums`으로 구현하는 일반적인 방법

```rust,editable
use crate::List::*;

enum List {    
    // Cons: 튜플 구조체로 요소 element와 다음 노드의 포인터를 갖고 있습니다.
    Cons(u32, Box<List>),
    // Nil: linked list의 끝을 나타내는 노드
    Nil,
}

// enum에는 method를 사용할 수 있습니다.
impl List {
    // 빈 리스트 생성
    fn new() -> List {
        // `Nil`은 `List`의 한 타입
        Nil
    }
    
    // list의 소유권을 가져와서, 새로운 요소를 리스트의 앞에 추가하여 리턴합니다.
    fn prepend(self, elem: u32) -> List {
        // `Cons` also has type List
        Cons(elem, Box::new(self))
    }
    
    // 리스트의 길이를 리턴
    fn len(&self) -> u32 {        
        // 이 메소드는 `self`의 유형에 의존하기 때문에 `self`는 패턴 매칭이 되어야만 합니다.
        // `self`는 `&List` 타입이고, `*self`는 `List` 타입입니다.
        // Rust 2018 이후로는 레퍼런스 `&T`로 매칭하기 보단 하는 타입 `T`로 매칭하는 것을 선호됩니다.
        // 아래 또한 self와 ref 없이 tail을 사용할 수 있고, rust는 &List와 ref tail을
        // 추론할 것 입니다.
        // 참고 https://doc.rust-lang.org/edition-guide/rust-2018/ownership-and-lifetimes/default-match-bindings.html
        match *self {            
            // `self`은 빌린 것이기 때문에 tail의 소유권을 가질 수 없습니다.
            Cons(_, ref tail) => 1 + tail.len(),
            // 기본 케이스 : 빈 리스트는 길이가 0
            Nil => 0
        }
    }
    
    // 리스트를 string 표현으로 리턴
    fn stringify(&self) -> String {
        match *self {
            Cons(head, ref tail) => {
                // `format!` 은 `print!`와 비슷하지만 heap에 할당된 string을 
                // 리턴하며, 콘솔에 프린트하지는 않습니다.
                format!("{}, {}", head, tail.stringify())
            },
            Nil => {
                format!("Nil")
            },
        }
    }
}

fn main() {
    // 빈 linked list 생성
    let mut list = List::new();

    // 각 요소를 리스트의 앞에서 추가합니다.
    list = list.prepend(1);
    list = list.prepend(2);
    list = list.prepend(3);

    // 리스트의 최종 상태를 보여줍니다.
    println!("linked list has length: {}", list.len());
    println!("{}", list.stringify());
}
```

### 참고:

[`Box`][box], [methods][methods]

[box]: ../../std/box.md
[methods]: ../../fn/methods.md
