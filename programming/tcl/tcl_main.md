# TCL

Old scripting language that is still being used in many companies because they have a lot of legacy code built on it.

This document will have some notes about how things work for future reference

## Procedures

Instead of using functions in TCL, we instead have procedures. They can be defined using the following syntax.

```tcl

proc name {arg1 arg2}  {

    return [expr $a+$b]
}
```

to call the function, do this:

```tcl

puts [name 10 40]
```

## Command syntax

### Commenting

You cannot do in-line comments in TCL.

```tcl
# Do this
puts [expr 10+11] #Not this
```

### Obtaining the result of a command

You are able to obtain the result of a command by using `[]`. Here is an example of how that works.

### Grouping Operator

`{}` is the grouping operator in TCL. This will either group a string together like `{hello world}` or a list like `{a b c d e f}`. It can also group scripts together, like `{ puts -nonewline {hello } puts world\n}`.

## Iteration

### Iterating over a list

The syntax for iterating over a list is foreach. Here is an example doing that.

```tcl
set values {1, 3, 5, 7, 8}
puts "Value\tSquare\tCube"
foreach x $values {
    puts " $x\t [expr {$x**2}]\t [expr {$x**3}]"
}
```

## Conditional

In programming you always find conditionals, so here is the syntax for this one:

```tcl
if { $a != $b } {
    # Do something
}
```