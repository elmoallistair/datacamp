## Regular Expressions for Pattern Matching

Time to discover the fundamental concepts of regular expressions! In this key chapter, you will learn to understand the basic concepts of regular expression syntax. Using a real dataset with tweets meant for sentiment analysis, you will learn how to apply pattern matching using normal and special characters, and greedy and lazy quantifiers.

<br>

### Are they bots?

```
# Import the re module
import re

# Write the regex
regex = r"@robot\d\W"

# Find all matches of regex
print(re.findall(regex, sentiment_analysis))
```

### Find the numbers

```
# Write a regex to obtain user mentions
print(re.findall(r"User_mentions:\d", sentiment_analysis))

# Write a regex to obtain user mentions
print(re.findall(r"likes:\s\d", sentiment_analysis))

# Write a regex to obtain user mentions
print(re.findall(r"number\sof\sretweets:\s\d", sentiment_analysis))
```

### Match and split

```
# Write a regex to match pattern separating sentences
regex_sentence = r"\W\dbreak\W"

# Replace the regex_sentence with a space
sentiment_sub = re.sub(regex_sentence, " ", sentiment_analysis)

# Write a regex to match pattern separating words
regex_words = r"\Wnew\w"

# Replace the regex_words and print the result
sentiment_final = re.sub(regex_words, "", sentiment_sub)
print(sentiment_final)
```

### Everything clean

```
# Import re module
import re

for tweet in sentiment_analysis:
	# Write regex to match http links and print out result
	print(re.findall(r"https:\S+", tweet))

	# Write regex to match user mentions and print out result
	print(re.findall(r"@\S+", tweet))
```

### Some time ago

```
# Complete the for loop with a regex to find dates
for date in sentiment_analysis:
	print(re.findall(r"\d{1,2}\s\S+\sago", date))

# Complete the for loop with a regex to find dates
for date in sentiment_analysis:
	print(re.findall(r"\d{1,2}\w{2}\s\S+\s\d{4}", date))

# Complete the for loop with a regex to find dates
for date in sentiment_analysis:
	print(re.findall(r"\d{1,2}\w{1,2}\s\S+\s\d{4}\s\d{1,2}:\d{2}",date))
```

### Getting tokens

```
# Write a regex matching the hashtag pattern
regex = r"#\w+"

# Replace the regex by an empty string
no_hashtag = re.sub(regex, "", sentiment_analysis)

# Get tokens by splitting text
print(re.split(r"\s+", no_hashtag))
```

### Finding files

```
# Write a regex to match text file name
regex = r"^[aeiouAEIOU]{2,3}\w+.txt"

for text in sentiment_analysis:
	# Find all matches of the regex
	print(re.findall(regex, text))
    
	# Replace all matches with empty string
	print(re.sub(regex, "", text))
```

### Give me your email

```
# Write a regex to match a valid email address
regex = r"^[a-zA-Z0-9!#%&*$.]+@\w+\.com"

for example in emails:
  	# Match the regex to the string
    if re.match(regex, example):
        # Complete the format method to print out the result
      	print("The email {email_example} is a valid email".format(email_example=example))
    else:
      	print("The email {email_example} is invalid".format(email_example=example))
```

### Invalid password

```
# Write a regex to match a valid password
regex = r"[a-zA-Z0-9*#$%!&.]{8,20}"

for example in passwords:
  	# Scan the strings to find a match
    if re.match(regex, example):
        # Complete the format method to print out the result
      	print("The password {pass_example} is a valid password".format(pass_example=example))
    else:
      	print("The password {pass_example} is invalid".format(pass_example=example))   
```

### Understanding the difference

```
# Import re
import re

# Write a regex to eliminate tags
string_notags = re.sub(r"<.+?>", "", string)

# Print out the result
print(string_notags)
```

### Greedy matching

```
# Write a lazy regex expression 
numbers_found_lazy = re.findall(r"\d+?", sentiment_analysis)

# Print out the result
print(numbers_found_lazy)

# Write a lazy regex expression 
numbers_found_greedy = re.findall(r"\d+", sentiment_analysis)

# Print out the result
print(numbers_found_greedy)
```

### Lazy approach

```
# Write a greedy regex expression to match 
sentences_found_greedy = re.findall(r"\(.+?\)", sentiment_analysis)

# Print out the result
print(sentences_found_greedy)

# Write a lazy regex expression
sentences_found_lazy = re.findall(r"\(.+?\)", sentiment_analysis)

# Print out the results
print(sentences_found_lazy)
```