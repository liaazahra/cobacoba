python
import numpy as np
from scipy import optimize

def f(x): return 3**x - 3*np.power(x, 2)

def find_root_with_tolerance(func, lower_bound, upper_bound, tolerance=0.005):
    def bisect_function(x):
        if func(x) * func((lower_bound + upper_bound)/2) < 0:
            return (upper_bound + lower_bound)/2
        elif abs(func((lower_bound + upper_bound)/2)) < tolerance:
            return (lower_bound + upper_bound)/2
        else:
            if func(lower_bound) * func((lower_bound + upper_bound)/2) < 0:
                return bisect_function(lower_bound+(upper_bound - lower_bound)/2)
            else:
                return bisect_function(upper_bound-(upper_bound - lower_bound)/2)
    
    initial_bounds = (lower_bound, upper_bound)
    result = optimize.bisect(bisect_function, *initial_bounds)
    return result.x

# Menjalankan fungsi find_root_with_tolerance
result = find_root_with_tolerance(f, -1, 1, tolerance=0.005)
print("Akar dari persamaan:", result)
