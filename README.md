# IJVM_Experiments

IJVM Assembly programs written in (Extended) Tanenbaum IJVM.

This repository contains some example programs written by me.
Part of these have been generated with a small toolchain I've written.

## IJVM implementation requirements

- [x] bfi2 uses extended instructions (NEWARRAY, IALOAD, IASTORE)
- [x] calc uses extensive recursion

## Files:

### calc

A reverse polish notation calculator with extensive feature set (not/and/or/xor/plus/minus/division/etc.)

Not a particularly complicated program but throws together a large number of operators.

### bfi2

A brainfuck interpreter, compiles the brainfuck to bytecode with some optimisations, and
and finally executes it. Works by giving it a

    bf_prog ":" bf_input

### mandelbread

A mandelbrot set viewer, the tricky part here is that IJVM obviously only has integers, and a very
limited set of arithmetic operations on these integers.

After constructing a mulitply that relies on the fact that `BIPUSH x; DUP; IADD` gives `2 * x`
and a slightly more involved division algorithm which works with the same principle,
we have the basic building blocks.

The rest of the algorithm is simply scaled up complex numbers (so theyre large enough for integer
calculations), and division at the right time. (Also comparison to 2 power is replaced with bitmasking)

In pseudocode (python), the core method would simply be (shifted 8 bits)

```python
def mandelbrot_int(real0, imag0, max_iterations):
    real, imag = real0, imag0

    for n in range(max_iterations):
        realq = (real * real) >> 8
        imagq = (imag * imag) >> 8

        #if (realq + imagq) >> (8 + 3) > 0:
        if (realq + imagq) & 0xfffff000 != 0:
            return n

        imag = ((real * imag) >> (8 - 1)) + imag0
        real = realq - imagq + real0

    return max_iterations
```

## Helpful links

- [My IJVM Layout inspector](https://workofartiz.github.io/ijvm/)
- [BlackNovaTech's Assembler](https://github.com/BlackNovaTech/goJASM)
- [BlackNovaTech's WebIJVM](https://apps.blacknova.io/webijvm/)


