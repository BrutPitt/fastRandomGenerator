# fastRandomGeneretor

**fastRandomGeneretor** is a  single and little header-only library for 32bit and 64bit FAST pseudoRandom generator, based on Marsaglia algorithms.

Just include 'fastRandom.h` in your code:
```C++
#include "fastRandom.h"
```

It includes two classes to generate `uint32_t/int32_t` and `uint64_t/int642_t` preudo-random numbers, based on KISS (Keep it Sample Stupid) and others algorithms of George Marsaglia.

Sources are well documented, and at the end of the file all the algorithms are explained, with links to author pages

All values are returned in interval `[0, UINT64_MAX]` for 64bit version and `[0, UINT32_MAX]` for 32bit version, but if you need (e.g.) values between `[INT32_MIN, INT32_MAX]`, just cast result to `int32_t` (and same for 64bit)

The classes are declared insde the namespace `fstRnd`

Alternative declaration (`typedef`) are provided for simplicity/abbreviation
``` C++
// 32 bit generator
using fastRand32 = fastRandom32Class;
// 64 bit generator
using fastRand64 = fastRandom64Class;

// single precision interface for 32 bit generator
using fFastRand32 = floatfastRandomClass<float,  fastRand32>;
// double precision interface for 32 bit generator
using dFastRand32 = floatfastRandomClass<double, fastRand32>;

// single precision interface for 64 bit generator
using fFastRand64 = floatfastRandomClass<float,  fastRand64>;
// double precision interface for 64 bit generator
using dFastRand64 = floatfastRandomClass<double, fastRand64>;
```

Example to use KISS 32bit algorithm:
``` C++
    fstRnd::fastRand32 fastRandom; // for 32bit
    for(int i=0; i<10000; i++)
        cout << fstRnd::fastRandom.KISS() << endl;
```

Both classes contain simplest and fastest `xorShift` (32/64 bit), as static member function.

Example to use static xorShift 64bit algorithm:
``` C++
    for(int i=0; i<10000; i++)
        cout << fstRnd::fastRand64::xorShift() << endl; // for 64bit
```

It includes also a *floating point* (single/double precision) template class, as a helper/front-end to generate fast numbers in `[-1.0, 1.0]` / `[0.0, 1.0]` / `[min, max]` intervals

Example use KISS 32bit algorithm in [-1.0, 1.0] interval, with double precision floating point:
``` C++
    fstRnd::dFastRand32 fastRandom; // for 32bit generator and double precision results [-1.0, 1.0]
    for(int i=0; i<10000; i++)
        cout << fstRnd::fastRandom.VNI() << endl;
```

Example use KISS 64bit algorithm in [min, max] interval, with single precision floating point:
``` C++
    const float fMin = -10.0, fMax=25.0;
    fstRnd::fFastRand64 fastRandom; // for 64bit generator and single precision results [fMin, fMax]
    for(int i=0; i<10000; i++)
        cout << fstRnd::fastRandom.range(fMin,fMax) << endl;
```

This library is currently used in [**glChAoS.P / wglChAoS.P](https://github.com/BrutPitt/glChAoS.P)

To generate DLA3D (Diffusion Limited Aggregation) - DLA 3D
[![](https://raw.githubusercontent.com/BrutPitt/glChAoS.P/master/screenShots/dla3D.jpg)](https://twitter.com/i/status/1120431893818769409)

And in Hypercomplex fractals with stochastic IIM (Inverse Iteration Method) algorithms 
[![](https://user-images.githubusercontent.com/16171743/50758310-1f231a80-1262-11e9-8065-3199292ff9f1.jpg)](https://www.michelemorrone.eu/glchaosp/Hypercomplex.html)