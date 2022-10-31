# 안녕 세상아<sup> Hello World</sup>

다음은 전통적인 Hello World 프로그램입니다.

```rust,editable
// 주석, 컴파일러는 이를 무시합니다.
// "Run" 버튼을 누르면, 테스트 해보실 수 있습니다.
// 키보드 사용를 선호하시면 "Ctrl + Enter" 단축키를 사용하실 수 있습니다. ->

// 코드는 수정이 가능하니 마음껏 수정하고 테스트 해보세요!
// "Reset" 버튼을 누르면 언제든지 원래 코드로 돌아갑니다. ->

// 메인 함수
fn main() {
    // 컴파일된 바이너리가 호출될때, 여기서부터 각 문장(statement)들이 실행됩니다.

    // 콘솔에 텍스트 출력
    println!("Hello World!");
}
```

`println!` 는 콘솔에 텍스트를 출력하는  [매크로][macros] 입니다.

Rust 컴파일러<sup>compiler</sup>는 바이너리<sup>binary</sup>를 생성합니다. : `rustc`.

```bash
$ rustc hello.rs
```

`rustc` 는 실행가능한 `hello` 바이너리를 생성합니다..

```bash
$ ./hello
Hello World!
```

### 실습

'Run' 버튼을 눌러 예상되는 출력이 나오는 지 확인해보세요. 그 다음에, 새로운
줄을 추가하고 `println!` 매크로를 사용해 아래처럼 결과가 나오게 해보세요.

```text
Hello World!
I'm a Rustacean!
```

[macros]: macros.md
