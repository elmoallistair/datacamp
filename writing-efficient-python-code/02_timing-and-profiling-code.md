## Timing and profiling code

In this chapter, you will learn how to gather and compare runtimes between different coding approaches. You'll practice using the line_profiler and memory_profiler packages to profile your code base and spot bottlenecks. Then, you'll put your learnings to practice by replacing these bottlenecks with efficient Python code.

<br>

### Using %timeit: your turn!

```
# Create a list of integers (0-50) using list comprehension
nums_list_comp = [num for num in range(51)]
print(nums_list_comp)

# Create a list of integers (0-50) by unpacking range
nums_unpack = [*range(51)]
print(nums_unpack)
```

### Using %timeit: formal name or literal syntax

```
# Create a list using the formal name
formal_list = list()
print(formal_list)

# Create a list using the literal syntax
literal_list = []
print(literal_list)

# Print out the type of formal_list
print(type(formal_list))

# Print out the type of literal_list
print(type(literal_list))
```

### Using %lprun: spot bottlenecks

```
%load_ext line_profiler
%lprun -f convert_units convert_units(heroes, hts, wts)
```

### Using %lprun: fix the bottleneck

```
%load_ext line_profiler
%lprun -f convert_units_broadcast convert_units_broadcast(heroes, hts, wts)
```

### Using %mprun: Hero BMI

```
%load_ext memory_profiler
from bmi_lists import calc_bmi_lists
%mprun -f calc_bmi_lists calc_bmi_lists(sample_indices, hts, wts)
```

### Using %mprun: Hero BMI 2.0

```
%load_ext memory_profiler
from bmi_arrays import calc_bmi_arrays
%mprun -f calc_bmi_arrays calc_bmi_arrays(sample_indices, hts, wts)
```

### Bringing it all together: Star Wars profiling

```
# Use get_publisher_heroes() to gather Star Wars heroes
star_wars_heroes = get_publisher_heroes(heroes, publishers, 'George Lucas')

print(star_wars_heroes)
print(type(star_wars_heroes))

# Use get_publisher_heroes_np() to gather Star Wars heroes
star_wars_heroes_np = get_publisher_heroes_np(heroes, publishers, 'George Lucas')

print(star_wars_heroes_np)
print(type(star_wars_heroes_np))


%load_ext line_profiler
%lprun star_wars_heroes
%lprun star_wars_heroes_np


%load_ext memory_profiler
from hero_funcs import get_publisher_heroes, get_publisher_heroes_np

%mprun -f get_publisher_heroes get_publisher_heroes(heroes, publishers, 'George Lucas')
%mprun -f get_publisher_heroes_np get_publisher_heroes_np(heroes, publishers, 'George Lucas')
```