---
layout: default
---

# Examples

## Defining a New Type of Matrix
```julia
struct SingleDiag{T <: Real} <: AbstractArray{T,2} # allows matrix operations
	diag::Array{T,1}
end

# Finding dimensions w/ size functions
Base.size(sd::SingleDiag) =
	(length(sd.diag), length(sd.diag))

# Using `[]` for access.
function getindex(sd::SingleDiag, indices::Vararg{Int,2})
	(i,j) = indices
	return i==j ? sd.diag[i] : 0
end

# Using `[]` for setting values.
function Base.setindex!(sd::SingleDiag, val, indices::Vararg{Int,2})
	(i,j) = indices
	if i != j
		error("Can't assign outside diag")
	end
	sd.diag[i] = val
	return sd
end

# Usage
s = SingleDiag{[1,2,3,4,5]}
@show size(s) # (5,5)
@show s[1,1] # 1
@show s[1,2] # 0
@show s[1,1] = 10
@show s # Singlediag{Int64}
        # ([10,2,3,4,5])
```
