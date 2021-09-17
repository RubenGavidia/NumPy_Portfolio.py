# NumPy_Portfolio.py
Matrices, Transpose, Inverse, Ortogonal, Product, Determinant, EigenValues, EigenVectors.


```
from random import randint
from numpy import array, append, zeros, ones, hstack, vstack, random
from operator import add, sub, mul, truediv
from timeit import timeit

def _print_result_as(title = '', items_to_print = {}):
  print('=== BEGIN %s ===\n' % (title))

  for key, value in items_to_print.items():
    print("%s\n %2s \n" % (key.upper(), value))

  print('=== END ===\n')

  print('*****************\n')


#######
# 1) Using exclusively numpy's zeros, ones, hstack, and 
# vstack functions, implement a function that 
# creates the following array and prints its 
# size and shape on the screen:

def initial_array():
  pair_of_ones = ones(2)
  pair_of_zeros = zeros(2)

  descending_row = hstack((pair_of_ones, pair_of_zeros))
  ascending_row = hstack((pair_of_zeros, pair_of_zeros))

  final_arr = vstack((
    descending_row,
    descending_row,
    ascending_row,
    ascending_row
  ))

  return {
    'final_arr':  final_arr,
    'shape': final_arr.shape,
    'size': final_arr.size
  }

# Calling function
_print_result_as('Ej. 1', initial_array())
#######

#######
# 2) # 3) Implement a function that receives two integer 
# parameters (n and m) and returns a two-dimensional 
#array of integers between 0 and 100 random. 

# Calling function
_print_result_as('Ej. 2', initial_array())

def random_arr(num_of_rows, num_of_columns):
  final_arr = []

  for i in range(0, num_of_rows):
    row = random.randint(0, 100, num_of_columns)
    final_arr.append(row)

  return vstack(final_arr)

print(random_arr(3, 2))

#######

#######
# 3) Implement a function that takes two parameters: 
# a two-dimensional n x m array of integers 
# (data type ndarray) and a scalar, and manually 
# diffuse the matrix with the scalar.n

def diffusion_arr(arr_to_use, scalar = 0, operation = '+'):
  math_mapping = { '+': add, '-': sub, '*': mul, '/': truediv }
  op = math_mapping.get(operation, '+')

  temp_arr = []

  for row in arr_to_use:
    updated_row = []

    for item in row:
      updated_row.append(op(item, scalar))

    temp_arr.append(updated_row)

  return (array(temp_arr))

# Calling function
arr_to_use = random_arr(num_of_rows = 3, num_of_columns = 2)
scalar = 3
operation = '+' # accepted values + - * /
_print_result_as('Ej. 3', {
  'arr_to_use': arr_to_use,
  'scalar': scalar,
  'operation': operation,
  'diffused_arr': diffusion_arr(arr_to_use, scalar, operation)
})
#######


#######
# 4) Using the previous functions, compare 
# the execution time of your function 
# implemented in the previous exercise 
# with the diffusion function of NumPy



def compare_time_arr(arr_to_use, scalar = 0, operation = '+'):
  math_mapping = { '+': add, '-': sub, '*': mul, '/': truediv }
  op = math_mapping.get(operation, '+')

  manual_diffusion = diffusion_arr(arr_to_use, scalar, operation)
  manual_diffusion_time = timeit(lambda: manual_diffusion, number = 1)

  numpy_diffusion = op(arr_to_use, scalar)
  numpy_diffusion_time = timeit(lambda: numpy_diffusion, number = 1)

  return {
    'manual_diffusion_time': f'{manual_diffusion_time} secs',
    'numpy_diffusion_time': f'{numpy_diffusion_time} secs'
  }

# Calling function
arr_scalar = randint(0, 100)
diff_operation = '+'

arr_10x10 = random_arr(num_of_rows = 10, num_of_columns = 10)
_print_result_as('Ej. 4.1 - 10x10', compare_time_arr(arr_10x10, arr_scalar, diff_operation))
-

arr_1000x1000 = random_arr(num_of_rows = 1000, num_of_columns = 1000)
_print_result_as('Ej. 4.2 - 1000x1000', compare_time_arr(arr_1000x1000, arr_scalar, diff_operation))

arr_10000x10000 = random_arr(num_of_rows = 10000, num_of_columns = 10000)
_print_result_as('Ej. 4.3 - 10000x10000', compare_time_arr(arr_10000x10000, arr_scalar, diff_operation))

```



