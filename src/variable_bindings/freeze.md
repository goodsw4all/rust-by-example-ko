# 동결 <sup>Freezing</sup>

같은 이름의 변수로 데이터를 불변성으로 바인딩 하면, 이전에 가변성으로 바인딩한 변수는 동결됩니다.
동결된 데이터는 불변성으로 바인딩한 변수가 볌위 밖으로 나갈 때 까지 수정이 불가능합니다.


```rust,editable,ignore,mdbook-runnable
fn main() {
    let mut _mutable_integer = 7i32;

    {
        // Shadowing by immutable `_mutable_integer`
        let _mutable_integer = _mutable_integer;

        // 현재 범위에서 `_mutable_integer`는 동결되었기 때문에 Error!
        // FIXME ^ 위의 주석을 제거하고 실행해보세요

        // `_mutable_integer`가 범위를 벗어납니다.
    }

    // Ok! `_mutable_integer` 
    _mutable_integer = 3;
}
```
