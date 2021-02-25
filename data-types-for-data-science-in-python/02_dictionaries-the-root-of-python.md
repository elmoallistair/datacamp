## Dictionaries - the root of Python

At the root of all things Python is a dictionary. Herein, you'll learn how to use them to safely handle data that can viewed in a variety of ways to answer even more questions about the New York Baby Names dataset. You'll explore how to loop through data in a dictionary, access nested data, add new data, and come to appreciate all of the wonderful capabilities of Python dictionaries.

<br>

### Creating and looping through dictionaries

```
# Create an empty dictionary: names_by_rank
names_by_rank = dict()

# Loop over the girl names
for rank, name in female_baby_names_2012.items():
    # Add each name to the names_by_rank dictionary using rank as the key
    names_by_rank[rank] = name
    
# Sort the names_by_rank dict by rank in descending order and slice the first 10 items
for rank in sorted(names_by_rank, reverse=True)[:10]:
    # Print each item
    print(names_by_rank[rank])
```

### Safely finding by key

```
# Safely print rank 7 from the names dictionary
print(names.get(7))

# Safely print the type of rank 100 from the names dictionary
print(type(names.get(100)))

# Safely print rank 105 from the names dictionary or 'Not Found'
print(names.get(105, "Not Found"))
```

### Dealing with nested data

```
# Print a list of keys from the boy_names dictionary
print(list(boy_names.keys()))

# Print a list of keys from the boy_names dictionary for the year 2013
print(list(boy_names[2013].keys()))

# Loop over the dictionary
for year in boy_names:
    # Safely print the year and the third ranked name or 'Unknown'
    print(year, boy_names[year].get(3, "Unknown"))
```

### Adding and extending dictionaries

```
# Assign the names_2011 dictionary as the value to the 2011 key of boy_names
boy_names[2011] = names_2011

# Update the 2012 key in the boy_names dictionary
boy_names[2012].update([(1, "Casey"), (2, "Aiden")])

# Loop over the years in the boy_names dictionary 
for year in boy_names:
    # Sort the data for each year by descending rank and get the lowest one
    lowest_ranked = sorted(boy_names[year], reverse=True)[0]
    # Safely print the year and the least popular name or 'Not Available'
    print(year, boy_names[year].get(lowest_ranked, "Not Available"))
```

### Popping and deleting from dictionaries

```
# Remove 2011 from female_names and store it: female_names_2011
female_names_2011 = female_names.pop(2011)

# Safely remove 2015 from female_names with an empty dictionary as the default: female_names_2015
female_names_2015 = female_names.pop(2015, {})

# Delete 2012 from female_names
del(female_names[2012])

# Print female_names
print(female_names)
```

### Working with dictionaries more pythonically

```
# Iterate over the 2014 nested dictionary
for rank, name in baby_names[2014].items():
    # Print rank and name
    print(rank, name)
    
# Iterate over the 2012 nested dictionary
for rank, name in baby_names[2012].items():
    # Print rank and name
    print(rank, name)
```

### Checking dictionaries for data

```
# Check to see if 2011 is in baby_names
if 2011 in baby_names:
    # Print 'Found 2011'
    print('Found 2011')
    
# Check to see if rank 1 is in 2012
if 1 in baby_names[2012]:
    # Print 'Found Rank 1 in 2012' if found
    print('Found Rank 1 in 2012')
else:
    # Print 'Rank 1 missing from 2012' if not found
    print('Rank 1 missing from 2012')
    
# Check to see if Rank 5 is in 2013
if 5 in baby_names[2013]:
   # Print 'Found Rank 5'
   print('Found Rank 5')
```

### Reading from a file using CSV reader

```
# Import the python CSV module
import csv

# Create a python file object in read mode for the baby_names.csv file: csvfile
csvfile = open("baby_names.csv", "r")

# Loop over a csv reader on the file object
for row in csv.reader(csvfile):
    # Print each row 
    print(row)
    # Add the rank and name to the dictionary
    baby_names[row[5]] = row[3]

# Print the dictionary keys
print(baby_names.keys())
```

### Creating a dictionary from a file

```
# Import the python CSV module
import csv

# Create a python file object in read mode for the `baby_names.csv` file: csvfile
csvfile = open("baby_names.csv", "r")

# Loop over a DictReader on the file
for row in csv.DictReader(csvfile):
    # Print each row 
    print(row)
    # Add the rank and name to the dictionary: baby_names
    baby_names[row["RANK"]] = row["NAME"]

# Print the dictionary keys
print(baby_names.keys())
```