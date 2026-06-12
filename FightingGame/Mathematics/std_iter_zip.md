#rust #rust_std #rust_std_iter

The `zip` method takes two separate iterators and fuses them into a single iterator that spits out pairs (tuples). Think of it exactly like a physical zipper on a jacket: it brings the left side and the right side together, tooth by tooth.

Here is the breakdown of how it works and its core behaviors:

### 1. Basic Mechanics

When you zip `Iterator A` and `Iterator B`, the first call to `next()` grabs the first element from A and the first element from B and returns them as `(a1, b1)`.


```rust
let a = [1, 2, 3];
let b = [4, 5, 6];

let mut zipped = a.into_iter().zip(b);

assert_eq!(zipped.next(), Some((1, 4)));
assert_eq!(zipped.next(), Some((2, 5)));
assert_eq!(zipped.next(), Some((3, 6)));
assert_eq!(zipped.next(), None);
```

### 2. The Shortest-Link Rule (Short-Circuiting)

If the two iterators are not the same length, `zip` stops as soon as **either** iterator runs out of elements. Any remaining elements in the longer iterator are ignored and not yielded.

```rust
let short = [1, 2];
let long = [9, 8, 7, 6];

let mut zipped = short.into_iter().zip(long);

assert_eq!(zipped.next(), Some((1, 9)));
assert_eq!(zipped.next(), Some((2, 8)));
assert_eq!(zipped.next(), None); // 'short' ran out, so zip finishes here.
```

### 3. Zipping with Infinite Ranges

Because it cuts off at the shortest iterator, `zip` is incredibly useful for pairing a finite collection with an infinite sequence, like `(0..)`. This acts similarly to the [.enumerate()](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.enumerate) method.

```rust
let words = ["foo", "bar"];
let zipper: Vec<(i32, &str)> = (0..).zip(words).collect();

// zipper is now vec![(0, "foo"), (1, "bar")]
```

### 4. Alternative Syntax: `std::iter::zip`

In the documentation page you are looking at, you will see a mention of a standalone function: `use std::iter::zip;`.

Instead of chaining `.zip()` onto the first iterator, you can pass both iterators as arguments to this function. It does the exact same thing but can be cleaner to read if your iterator chains are already very long or complex:


```rust
// Method chain style
let variant_a = a.into_iter().map(|x| x * 2).zip(b);

// Standalone function style
let variant_b = std::iter::zip(a.into_iter().map(|x| x * 2), b);
```