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