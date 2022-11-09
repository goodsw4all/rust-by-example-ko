# 튜플 <sup>Tuples</sup>

튜플은 서로 다른 타입의 값들의 집합입니다. 튜플은 소괄호`()`를 사용하여 구성합니다. 
`T1`, `T2` 멤버들의 자료형이라고 한다면 튜플은 `(T1, T2, ...)` 의 형태로 값을 가지게 됩니다.
함수에서는 튜플을 이용해 여러 개의 값을 리턴할 수 있습니다. 튜플은 여러 개의 값을 저장할 수 
있기 때문입니다.

```rust,editable
// 튜플은 인수와 리턴값으로 사용될 수 있습니다.
fn reverse(pair: (i32, bool)) -> (bool, i32) {
    // `let` 키워드는 튜플의 멤버들을 변수에 연결하는 데 사용됩니다.
    let (int_param, bool_param) = pair;

    (bool_param, int_param)
}

// 다음 구조체는 실습을 위한 것 입니다.
#[derive(Debug)]
struct Matrix(f32, f32, f32, f32);

fn main() {
    // 다양한 자료형으로 구성한 튜플
    let long_tuple = (1u8, 2u16, 3u32, 4u64,
                      -1i8, -2i16, -3i32, -4i64,
                      0.1f32, 0.2f64,
                      'a', true);

    // 튜플 인덱싱을 사용하면 튜플에서 값을 꺼낼 수 있습니다.
    println!("long tuple first value: {}", long_tuple.0);
    println!("long tuple second value: {}", long_tuple.1);

    // 튜플은 튜플의 멤버가 될 수 있습니다.
    let tuple_of_tuples = ((1u8, 2u16, 2u32), (4u64, -1i8), -2i16);

    // 튜플은 프린트 할 수 있습니다.
    println!("tuple of tuples: {:?}", tuple_of_tuples);
        
    // 하지만, 12개 이상의 긴 튜플은 프린트 되지 않습니다.
    // let too_long_tuple = (1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13);
    // println!("too long tuple: {:?}", too_long_tuple);
    // TODO ^ 컴파일 에러를 확인하려면, 위의 2줄의 주석을 제거해보세요.

    let pair = (1, true);
    println!("pair is {:?}", pair);

    println!("the reversed pair is {:?}", reverse(pair));

    // 한 개의 멤버로 구성된 튜플을 만드려면, 괄호 안에 있는 리터럴들과 구분하기 위해
    // 컴마가 필요합니다.
    println!("one element tuple: {:?}", (5u32,));
    println!("just an integer: {:?}", (5u32));
    
    // 튜플은 변수와 연결하기 위해 해체할 수 있습니다.
    let tuple = (1, "hello", 4.5, true);

    let (a, b, c, d) = tuple;
    println!("{:?}, {:?}, {:?}, {:?}", a, b, c, d);

    let matrix = Matrix(1.1, 1.2, 2.1, 2.2);
    println!("{:?}", matrix);

}
```

### 실습

 1. **개요**: `fmt::Display` 트레이트를 위에 있는 `Matrix`에 추가해서, 
    디버그 포맷 `{:?}` 을 디스플레이 포맷 `{}`으로 변경해 다음과 같은 결과를 출력해보세요.

    ```text
    ( 1.1 1.2 )
    ( 2.1 2.2 )
    ```

    [print display][print_display]의 예제를 참고하셔도 좋습니다.

 2. `reverse` 를 참고해 `transpose` 를  구현해서, matrix를 인자로 하고, 2개의 요소가
    스왑된 matrix를 리턴해보세요. 예는 다음과 같습니다.

    ```rust,ignore
    println!("Matrix:\n{}", matrix);
    println!("Transpose:\n{}", transpose(matrix));
    ```

    출력 결과:

    ```text
    Matrix:
    ( 1.1 1.2 )
    ( 2.1 2.2 )
    Transpose:
    ( 1.1 2.1 )
    ( 1.2 2.2 )
    ```

[print_display]: ../hello/print/print_display.md
