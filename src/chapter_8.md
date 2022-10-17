# Chapter 8: Streaming vs. Complete Parsers

Sometimes, we don't have the whole output at our disposal. For instance, 
we might be streaming input over the internet. To deal with this, nom 
allows for "streaming" parsers. They do not assume they have all the input,
so you can give them partial inputs and they will return different errors
based on whether they are _definitely_ finished (successfully or otherwise),
or whether they need more input.

Many parsers we have used so far have been from a `::complete`package. These 
packages always assume they have the whole input. They generally have a 
corresponding `::streaming`package, which does not make that assumption.

For example, we saw the `tag`  parser in [Chapter 2](./chapter_2.md). 
You can see a use of it below; in both a streaming and a complete fashion.
Where the tag splits over two lines, 

```rust
# extern crate nom;
# pub use nom::IResult;
# use std::error::Error;

fn parse_complete(input: &str) -> IResult<&str, &str> {
    use nom::bytes::complete::tag;
    tag("abc\ndef")(input)
}

fn parse_streaming(input: &str) -> IResult<&str, &str> {
    use nom::bytes::streaming::tag;
    tag("abc\ndef")(input)
}
fn main() -> Result<(), Box<dyn Error>> {
    let lines = vec!["abc\n", "def\n"];
    let bad_tag_lines = vec!["abc\n", "df\n"];
    
    for line in lines {
    }
#   Ok(())
}
```
