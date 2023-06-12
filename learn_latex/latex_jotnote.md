---
tags: latex, math, learning
---

# LaTeX Random notes

These are my notes that I am taking as I am doing LaTeX exercises.

## Metadata

Here are some stuff that you would have to setup before beginning to write the actual content.

```LaTeX
\title{Hello World!} % We use percent sign to write comments in LaTeX
\documentclass{article} % This is how you can use preset formatting
\author{Bach Wongwandanee} % Here is how you assign an author to a document
\date{\today} % Either actually type in the date or use \today to get the date

```

The data assigned into the metadata will not show up on the compiled document unless you choose to place them there yourself.

## Document basics

To actually start writing the content of the documents, you need to place the text in this enclosure.
```latex
\begin{document}
\maketitle % This will render all the metadata that are related to the title
% Text here
\end{document}
```

### Creating math blocks

```latex
$ a^2 + b^2 = c^2 $ % This is the inline math block
$$ % This is an unlabeled math block. It lets you write math equation, but no tracking.
\vec{\omega}\cdot\vec{\delta} = \vec{\theta}
$$

\begin{equation}  % These are tracked math blocks. They will have an equation sign
\end{equation}
```

Here are some examples of the above math blocks. The in-line math block: $a^2+b^2=c^2$.

A full untracked math block:

$$
\vec{\omega}\cdot\vec{\delta} = \vec{\theta}
$$

## Math methods

There are some basics that you would need to know to be able to write LaTeX math, here are some important ones.

```latex
\vec{E} % This will give whatever is enclosed a vector arrow on top
```