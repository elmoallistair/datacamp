## Handling Dates and Times

Handling times can seem daunting at time, but here, you'll dig in and learn how to create datetime objects, print them, look to the past and to the future. Additionally, you'll learn about some third party modules that can make all of this easier. You'll continue to use the Chicago Transit dataset to answer questions about transit times.

<br>

### Strings to DateTimes

```
# Import the datetime object from datetime
from datetime import datetime

# Iterate over the dates_list 
for date_str in dates_list:
    # Convert each date to a datetime object: date_dt
    date_dt = datetime.strptime(date_str, "%m/%d/%Y")
    
    # Print each date_dt
    print(date_dt)
```

### Converting to a String

```
# Loop over the first 10 items of the datetimes_list
for item in datetimes_list[:10]:
    # Print out the record as a string in the format of 'MM/DD/YYYY'
    print(item.strftime("%m/%d/%Y"))
    
    # Print out the record as an ISO standard string
    print(item.isoformat())
```

### Pieces of Time

```
# Create a defaultdict of an integer: monthly_total_rides
monthly_total_rides = defaultdict(int)

# Loop over the list daily_summaries
for daily_summary in daily_summaries:
    # Convert the service_date to a datetime object
    service_datetime = datetime.strptime(daily_summary[0],"%m/%d/%Y")

    # Add the total rides to the current amount for the month
    monthly_total_rides[service_datetime.month] += int(daily_summary[4])
    
# Print monthly_total_rides
print(monthly_total_rides)
```

### Creating DateTime Objects... Now

```
# Import datetime from the datetime module
from datetime import datetime

# Compute the local datetime: local_dt
local_dt = datetime.now()

# Print the local datetime
print(local_dt)

# Compute the UTC datetime: utc_dt
utc_dt = datetime.utcnow()

# Print the UTC datetime
print(utc_dt)
```

### Timezones

```
# Create a Timezone object for Chicago
chicago_usa_tz = timezone("US/Central")

# Create a Timezone object for New York
ny_usa_tz = timezone("US/Eastern")

# Iterate over the daily_summaries list
for orig_dt, ridership in daily_summaries:

    # Make the orig_dt timezone "aware" for Chicago
    chicago_dt = orig_dt.replace(tzinfo=chicago_usa_tz)
    
    # Convert chicago_dt to the New York Timezone
    ny_dt = chicago_dt.astimezone(ny_usa_tz)
    
    # Print the chicago_dt, ny_dt, and ridership
    print('Chicago: %s, NY: %s, Ridership: %s' % (chicago_dt, ny_dt, ridership))
```

### Finding a time in the future and from the past

```
# Import timedelta from the datetime module
from datetime import timedelta

# Build a timedelta of 30 days: glanceback
glanceback = timedelta(days=30)

# Iterate over the review_dates as date
for date in review_dates:
    # Calculate the date 30 days back: prior_period_dt
    prior_period_dt = date - glanceback
    
    # Print the review_date, day_type and total_ridership
    print('Date: %s, Type: %s, Total Ridership: %s' %
         (date, 
          daily_summaries[date]['day_type'], 
          daily_summaries[date]['total_ridership']))

    # Print the prior_period_dt, day_type and total_ridership
    print('Date: %s, Type: %s, Total Ridership: %s' %
         (prior_period_dt, 
          daily_summaries[prior_period_dt]['day_type'], 
          daily_summaries[prior_period_dt]['total_ridership']))
```

### Finding differences in DateTimes

```
# Iterate over the date_ranges
for start_date, end_date in date_ranges:
    # Print the End and Start Date
    print(end_date, start_date)
    # Print the difference between each end and start date
    print(end_date - start_date)
```

### Localizing time with pendulum

```
# Import the pendulum module
import pendulum

# Create a now datetime for Tokyo: tokyo_dt
tokyo_dt = pendulum.now("Asia/Tokyo")

# Covert the tokyo_dt to Los Angeles: la_dt
la_dt = tokyo_dt.in_timezone("America/Los_Angeles")

# Print the ISO 8601 string of la_dt
print(la_dt.to_iso8601_string())
```

### Humanizing Differences with Pendulum

```
# Iterate over date_ranges
for start_date, end_date in date_ranges:

    # Convert the start_date string to a pendulum date: start_dt 
    start_dt = pendulum.parse(start_date, strict=False)
    
    # Convert the end_date string to a pendulum date: end_dt 
    end_dt = pendulum.parse(end_date, strict=False)
    
    # Print the End and Start Date
    print(end_dt, start_dt)
    
    # Calculate the difference between end_dt and start_dt: diff_period
    diff_period = end_dt - start_dt
    
    # Print the difference in days
    print(diff_period.in_days())
```