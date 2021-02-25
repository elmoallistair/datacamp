## Fundamental data types

This chapter will introduce you to the fundamental Python data types - lists, sets, and tuples. These data containers are critical as they provide the basis for storing and looping over ordered data. To make things interesting, you'll apply what you learn about these types to answer questions about the New York Baby Names dataset!

<br>

### Manipulating lists for fun and profit

```
# Create a list containing the names: baby_names
baby_names = ["Ximena", "Aliza", "Ayden", "Calvin"]

# Extend baby_names with 'Rowen' and 'Sandeep'
baby_names.extend(["Rowen", "Sandeep"])

# Print baby_names
print(baby_names)

# Find the position of 'Aliza': position
position = baby_names.index("Aliza")

# Remove 'Aliza' from baby_names
baby_names.pop(1)

# Print baby_names
print(baby_names)
```

### Looping over lists

```
# Create the empty list: baby_names
baby_names = list()

# Loop over records 
for name in records:
    # Add the name to the list
    baby_names.append(name[3])
    
# Sort the names in alphabetical order
for name in sorted(baby_names):
    # Print each name
    print(name)
```

### Data type usage

```
Q: Which data type would you use if you wanted your data to be immutable and ordered?
A: Tuple
```

### Using and unpacking tuples

```
# Pair up the girl and boy names: pairs
pairs = zip(girl_names, boy_names)

# Iterate over pairs
for idx, pair in enumerate(pairs):
    # Unpack pair: girl_name, boy_name
    girl_name, boy_name = pair
    # Print the rank and names associated with each rank
    print('Rank {}: {} and {}'.format(idx, girl_name, boy_name))
```

### Making tuples by accident

```
# Create the normal variable: normal
normal = "simple"

# Create the mistaken variable: error
error = "trailing comma",

# Print the types of the variables
print(type(normal))
print(type(error))
```

### Finding all the data and the overlapping data between sets

```
# Find the union: all_names
all_names = baby_names_2011.union(baby_names_2014)

# Print the count of names in all_names
print(len(all_names))

# Find the intersection: overlapping_names
overlapping_names = baby_names_2011.intersection(baby_names_2014)

# Print the count of names in overlapping_names
print(len(overlapping_names))
```

### Determining set differences

```
# Create the empty set: baby_names_2011
baby_names_2011 = set()

# Loop over records and add the names from 2011 to the baby_names_2011 set
for row in records:
    # Check if the first column is '2011'
    if row[0] == '2011':
        # Add the fourth column to the set
        baby_names_2011.add(row[3])

# Find the difference between 2011 and 2014: differences
differences = baby_names_2011.difference(baby_names_2014)

# Print the differences
print(differences)
```