# QuTiP.jl

<!-- 
[![Build Status](https://travis-ci.org/goropikari/QuTiP.jl.svg?branch=master)](https://travis-ci.org/goropikari/QuTiP.jl)

[![Coverage Status](https://coveralls.io/repos/goropikari/QuTiP.jl/badge.svg?branch=master&service=github)](https://coveralls.io/github/goropikari/QuTiP.jl?branch=master)

[![codecov.io](http://codecov.io/github/goropikari/QuTiP.jl/coverage.svg?branch=master)](http://codecov.io/github/goropikari/QuTiP.jl?branch=master)
-->

This package is a wrapper of [QuTiP](http://qutip.org/) using [PyCall](https://github.com/stevengj/PyCall.jl).


# Install

```julia
Pkg.clone("https://github.com/goropikari/QuTiP.jl")
```

# Translate Python code into Julia code
Almost all syntax is same as original QuTiP, but some features are different. 
As [PyCall](https://github.com/JuliaPy/PyCall.jl)'s troubleshooting says, use `foo[:bar]` and `foo[:bar](...)` rather than `foo.bar` and `foo.bar(...)`, respectively.

```python
# python
# quoted from [QuTiP tutorial](http://nbviewer.jupyter.org/github/qutip/qutip-notebooks/blob/master/examples/superop-contract.ipynb)
import numpy as np
import qutip as qt
%matplotlib inline
qt.settings.colorblind_safe = True

q = basis(2,0)
q.dag()

qt.visualization.hinton(qt.identity([2, 3]).unit());
```

```julia
# julia
using QuTiP, PyPlot

q = basis(2,0)
q[:dag]() # or dag(q)

hinton(qidentity([2, 3])[:unit]()) # instead of identity use qidentity
```

# convert Qobj to Julia array
To convert Oobj to julia array, use `full`.
```julia
julia> x = basis(2,0)
PyObject Quantum object: dims = [[2], [1]], shape = (2, 1), type = ket
Qobj data =
[[ 1.]
 [ 0.]]

julia> x[:full]()
2×1 Array{Complex{Float64},2}:
 1.0+0.0im
 0.0+0.0im

julia> sigmax()[:full]()
2×2 Array{Complex{Float64},2}:
 0.0+0.0im  1.0+0.0im
 1.0+0.0im  0.0+0.0im
```

# Renamed functions
In order to avoid name conflict, some functions are rennamed.  
original name --> renamed
- position --> qposition
- identity --> qidentity
