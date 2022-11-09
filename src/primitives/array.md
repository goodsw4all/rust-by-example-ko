# 배열과 슬라이스 <sup>Slices</sup>

배열 <sup>array</sup>은 연속된 메모리에 저장되고, 동일한 자료형 `T` 객체의 집합입니다.
배열은 대괄호 `[]`를 사용하고, 배열의 길이는 컴파일 타임에 결정됩니다. `[T; length]`

슬라이스는 배열과 유사하지만 컴파일 타임에 길이를 알 수 없습니다. 대신, 슬라이스는 2워드 객체입니다.
첫번째 워드는 데이터를 가르키는 포인터이고, 두번째 워드는 슬라이스의 길이 입니다.
워드의 크기는 usize 와 같고 프로세서 아키텍처에 따라 다릅니다. 예) x86-64의 워드크기는 65비트  
슬라이스는 배열의 한 구역을 빌릴<sup>borrow</sup> 수 있고, `&[T]` 와 같은 형태를 가집니다.

```rust,editable,ignore,mdbook-runnable
use std::mem;

// 다음 함수는 슬라이스를 빌립니다.
fn analyze_slice(slice: &[i32]) {
    println!("first element of the slice: {}", slice[0]);
    println!("the slice has {} elements", slice.len());
}

fn main() {    
    // 고정크기의 배열 (자료형 시그니처는 불필요 합니다.)
    let xs: [i32; 5] = [1, 2, 3, 4, 5];
    
    // 모든 요소를 같은 값으로 초기화할 수 있습니다.
    let ys: [i32; 500] = [0; 500];

    // 인덱스는 0 부터 시작합니다.
    println!("first element of the array: {}", xs[0]);
    println!("second element of the array: {}", xs[1]);

    // `len` 함수는 배열의 총 요소 개수를 리턴합니다.
    println!("number of elements in array: {}", xs.len());

    // 배열은 스택에 할당됩니다.
    println!("array occupies {} bytes", mem::size_of_val(&xs));
    
    // 자동적으로 배열은 슬라이스로 빌려질 수 있습니다.
    println!("borrow the whole array as a slice");
    analyze_slice(&xs);

    // 슬라이스는 배열의 한 구역을 가르키고,   
    // 형식은 [starting_index..ending_index] 입니다.
    // starting_index는 슬라이스의 첫번째 위치이고, ending_index는 슬라이스의
    // 마지막 위치 +1 입니다.
    println!("borrow a section of the array as a slice");
    analyze_slice(&ys[1 .. 4]);

    // 빈 슬라이스 `&[]`
    let empty_array: [u32; 0] = [];
    assert_eq!(&empty_array, &[]);
    assert_eq!(&empty_array, &[][..]); // 같지만 좀 더 자세히

    // 배열은 `.get`함수를 사용하면 안전하게 액세스 할 수 있습니다. 
    // `.get`함수는 `Option`을 리턴합니다. 아래에서 보여지듯이 match를 사용하거나
    // 행복하게 실행을 계속하는 대신 친절한 메시지와 함께 끝내고 싶다면
    // `.expect()`를 사용할 수 있습니다.
    for i in 0..xs.len() + 1 { // 웁스, 한개의 요소만큼 멀리 떨어져 있음
        match xs.get(i) {
            Some(xval) => println!("{}: {}", i, xval),
            None => println!("Slow down! {} is too far!", i),
        }
    }

    // 바운드를 벗어난 인덱싱은 런타임에러를 발생시킵니다.
    //println!("{}", xs[5]);
}
```
