# `enum`

## Definition

Enums let you say that a value if one of a possible list.

For example, you can say that `retangle` is one of possible `shapes` and you can also have `circles` or `triangles`. This is how rust works with `enums`.

Another use-case is IP protocols, as IPv4 and IPv6 are the main protocols that are currently being used often, we are able to say that an IP could be either IPv4 or IPv6. Here is an example:

```rust
enum IPAddr  {
	V4,
	V6,
}
```

So how do we use our type? Here is an example

```rust
let ip_1 = IPAddr::V4;
let ip_2 = IPAddr::V6;
```

This allows for easy function passes, since Rust will see `IPAddr` as the type, so you won't have to specify. Here is that example for passing an `enum` type into a function.

```rust
fn socket(ip_addr: IPAddr)  {}
```

You can call these functions like below:

```rust
socket(IPAddr::V4);
socket(IPAddr::V6);
```

In the above example, we are essentially using the `enum` type as the value that is being passed, but what if we want the type to be able to hold value as well?

Here is an example of how you make the `enum` hold value as well as the type.

# Links
