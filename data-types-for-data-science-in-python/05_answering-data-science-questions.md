## Answering Data Science Questions 

Time for a case study to reinforce all of your learning so far! You'll use all the containers and data types you've learned about to answer several real world questions about a dataset containing information about crime in Chicago. Have fun!

<br>

### Reading your data with CSV Reader and Establishing your Data Containers

```
# Import the csv module
import csv

# Create the file object: csvfile
csvfile = open("crime_sampler.csv", "r")

# Create an empty list: crime_data
crime_data = []

# Loop over a csv reader on the file object
for row in csv.reader(csvfile):
    # Append the date, type of crime, location description, and arrest
    crime_data.append((row[0], row[2], row[4], row[5]))
    
# Remove the first element from crime_data
crime_data.pop(0)

# Print the first 10 records
print(crime_data[:10])
```

### Find the Months with the Highest Number of Crimes

```
# Import necessary modules
from collections import Counter
from datetime import datetime

# Create a Counter Object: crimes_by_month
crimes_by_month = Counter()

# Loop over the crime_data list
for data in crime_data:
    
    # Convert the first element of each item into a Python Datetime Object: date
    date = datetime.strptime(data[0], '%m/%d/%Y %I:%M:%S %p')
    
    # Increment the counter for the month of the row by one
    crimes_by_month[date.month] += 1
    
# Print the 3 most common months for crime
print(crimes_by_month.most_common(3))
```

### Transforming your Data Containers to Month and Location

```
# Import necessary modules
from collections import defaultdict
from datetime import datetime

# Create a dictionary that defaults to a list: locations_by_month
locations_by_month = defaultdict(list)

# Loop over the crime_data list
for row in crime_data:
    # Convert the first element to a date object
    date = datetime.strptime(row[0], '%m/%d/%Y %I:%M:%S %p')
    
    # If the year is 2016 
    if date.year == 2016:
        # Set the dictionary key to the month and append the location (fifth element) to the values list
        locations_by_month[date.month].append(row[4])
    
# Print the dictionary
print(locations_by_month)
```

### Find the Most Common Crimes by Location Type by Month in 2016

```
# Import Counter from collections
from collections import Counter

# Loop over the items from locations_by_month using tuple expansion of the month and locations
for month, locations in locations_by_month.items():
    # Make a Counter of the locations
    location_count = Counter(locations)
    # Print the month 
    print(month)
    # Print the most common location
    print(location_count.most_common(5))
```

### Reading your Data with DictReader and Establishing your Data Containers

```
# Create the CSV file: csvfile
csvfile = open("crime_sampler.csv", "r")

# Create a dictionary that defaults to a list: crimes_by_district
crimes_by_district = defaultdict(list)

# Loop over a DictReader of the CSV file
for row in csv.DictReader(csvfile):
    # Pop the district from each row: district
    district = row.pop("District")
    # Append the rest of the data to the list for proper district in crimes_by_district
    crimes_by_district[district].append(row)
```

### Determine the Arrests by District by Year

```
# Loop over the crimes_by_district using expansion as district and crimes
for district, crimes in crimes_by_district.items():
    # Print the district
    print(district)
    
    # Create an empty Counter object: year_count
    year_count = Counter()
    
    # Loop over the crimes:
    for crime in crimes:
        # If there was an arrest
        if crime["Arrest"] == "true":
            # Convert the Date to a datetime and get the year
            year = datetime.strptime(crime["Date"], '%m/%d/%Y %I:%M:%S %p').year
            # Increment the Counter for the year
            year_count[year] += 1
            
    # Print the counter
    print(year_count)
```

### Unique Crimes by City Block

```
# Create a unique list of crimes for the first block: n_state_st_crimes
n_state_st_crimes = set(crimes_by_block['001XX N STATE ST'])

# Print the list
print(n_state_st_crimes)

# Create a unique list of crimes for the second block: w_terminal_st_crimes
w_terminal_st_crimes = set(crimes_by_block['0000X W TERMINAL ST'])

# Print the list
print(w_terminal_st_crimes)

# Find the differences between the two blocks: crime_differences
crime_differences = n_state_st_crimes.difference(w_terminal_st_crimes)

# Print the differences
print(crime_differences)
```