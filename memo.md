## パターンマッチングについて
https://doc.rust-lang.org/book/ch19-00-patterns.html
深い...

```
let optional_point = Some(Point { x: 100, y: 200 });

    // Solution 1: Matching over the `Option` (not `&Option`) but without moving
    // out of the `Some` variant.
    match optional_point {
        Some(ref p) => println!("Co-ordinates are {},{}", p.x, p.y),
        //   ^^^ added
        _ => panic!("No match!"),
    }

    // Solution 2: Matching over a reference (`&Option`) by added `&` before
    // `optional_point`.
    match &optional_point {
        Some(p) => println!("Co-ordinates are {},{}", p.x, p.y),
        _ => panic!("No match!"),
    }
```

https://stackoverflow.com/questions/68063555/when-to-use-ref-in-rust

```
fn new(value: i64) -> Result<Self, CreationError> {
        match value.cmp(&0) {
            Ordering::Less => Err(CreationError::Negative),
            Ordering::Equal => Err(CreationError::Zero),
            Ordering::Greater => Ok(Self(value as u64)),
        }
    }
```

##　ライフタイムについて
Lifetimekataやってもいい

## Iteratorの大事なところ
into_iter()　コレクションへの所有権消費、元の要素の値そのものを返す
    - ``` for item in collection {}```という構文は、内部でinto_iter()を呼び出している。
iter() 所有権を消費せず、要素への普遍参照を返す
iter_mut()　所有権を消費せず、要素への可変参照を返す。


## Stringってコレクションなの？
広義にはコレクション。でも、バイトのシーケンスを所有する型。でも、パフォーマンスがO(1)にならないのでインデックスアクセスは不可。
### Iterは実装されてない？
String型にはiter()という名前では定義されてないが、&strにはいてレーター生成メソッドが定義されている。
- chars() -> Iterator<item = cahr>
- bytes() -> Iterator<item = u8>
- bytes() -> Iterator<item = (usize, char)>
など。iter()という名前で実装されていないのは、いろんな返り値の方の可能性があり、一位に定まらないから？(ex. Vic<T>の場合はTという型に定まる)