Automatically modify programs so that they optimize for some resources.
- run faster, use less memory, use less power
For example, `X = Y*0` is the same as `X = 0`

Realistically, we are trying to:
- eliminate dead-code which is removing code that never executes
- register allocation and cache-aware optimizations
- use of special-purpose instructions e.g. graphics, FFT

A typical optimization by compilers is **code propagation**
```
a = b 
c = 2 + a
```
This becomes:
```
a = b 
c = 2 + b
```

A typical optimization by compilers is removing constants from being calculated during runtime:
```
a = 1.732
b = 1.414
c = a + b
```
The compiler has to do extra calculation during runtime to add these constants which can be saved by doing the computation myself. However, these optimizations can cause unwanted side effects. See: [Security flaws caused by compiler optimizations](https://www.redhat.com/en/blog/security-flaws-caused-compiler-optimizations)
