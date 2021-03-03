## Introduction to HTML

Learn the structure of HTML. We begin by explaining why web scraping can be a valuable addition to your data science toolbox and then delving into some basics of HTML. We end the chapter by giving a brief introduction on XPath notation, which is used to navigate the elements within HTML code.

<br>

### From Tree to HTML

```
html = '''
<html>
  <head>
    <title>Intro HTML</title>
  </head>
  <body>
    <p>Hello World!</p>
    <p>Enjoy DataCamp!</p>
  </body>
</html>
'''
```

### Keep it Classy

```
# HTML code string
html = '''
<html>
  <body>
    <div class="class1" id="div1">
      <p class="class2">Visit DataCamp!</p>
    </div>
    <div class="you-are-classy">
      <p class="class2">Keep up the good work!</p>
    </div>
  </body>
</html>
'''

# Print out the class of the second div element
whats_my_class( html )
```

### Where am I?

```
# Fill in the blank
xpath = '/html/body/div[2]/p'
```

### It's Time to P

```
# Fill in the blank
xpath = "//p"
```

### A classy span

```
# Fill in the blank
xpath = "//span[@class='span-class']"
```