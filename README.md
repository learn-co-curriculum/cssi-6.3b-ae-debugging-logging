

#Google App Engine: Logging and Debugging

##Debugging

+ Here we have a main.py script with an error in it.

```python
class MainHandler(webapp2.RequestHandler):
  def get(self):
    message = 'Hello, World!' - 8
    self.response.write(message)
```
If we try to run this code we will get a blank page, now what?

##The Mindset of Debugging
<img src="http://collectskin.com/wp-content/uploads/2010/07/killbug.png" width="300px">

The process of writing code is the process of debugging. As a programmer, you will always be looking for bugs to fix.

In GoogleAppEngineLauncher, pressing the **Logs** button will open the **Log Console** window, which will show your error messages.

<kbd style="color:red">ERROR    2015-06-17 22:19:45,960 cgi.py:122] Traceback (most recent call last):</br>
  File "/Users/Development/appengine-practice/main.py", line 6, in module</br>
    print 'Hello, world!' - 8</br>
TypeError: cannot concatenate 'str' and 'int' objects</kbd>

+ The error messages include information that tells you which file you are actually running and where it is located. Always check and be sure you are running and working on the file you think you are!


#Partner Programming Exercise 1:
Copy and paste the following into main.py. It contains a couple errors! Use the console to find and fix the errors.

```python
if true:
  self.response.write(
    'The truth will set you free.')
else
  self.response.write(
    'How did I get here?')
```

#Partner Programming Exercise 2:

Partner Exercise 2: This longer program contains more than one error. Copy and paste it into main.py  
Use the console to help you track them down, and fix them all.
```python
def TalkLikeAJedi(sentence):
  """Converts a sentence to Jedi-speak. Adapted from Python 3 for Absolute Beginners: http://www.google.com/books?id=sQGFIX_0xCUC&pg=PA242"""
  # Strip whitespace and punctuation
  sentence = sentence.strip().rstrip('.!')
  # Lowercase the first letter of the sentence
  sentence = sentence[0].lower() + sentence[1:]
  # Piratify the text
  sentence = 'Patience, ' + sentance + ', my young padawan.'
  
  retunn sentence

#put inside handler
sentence = 'Hello, world!'
self.response.write(TalkLikeAJEdi(sentence))
```

##Logging
Logging is a means of tracking events that happen when a program runs.The logging module lets you write messages directly to the console instead of sending them to the browser.

You can use the logging module by importing it at the top of your script:  <kbd>import logging</kbd>

It allows you to add logging statements to your script. Like this:
```python
logging.info('Hello, doing some logging!')
```
Once the page is reloaded, the logging statement will appear in the log console.

#Partner Programming Logging Exercise 1:
Try copy and pasting this script into main.py:
```python
import logging

def IsPrime(n):
  """A simple (but inefficient) check to see whether a number is prime."""
  for possible_factor in range(1, n):
    if n % possible_factor == 0:
      return False
  return True

#put in handler
n = 100
if IsPrime(n):
  self.response.write('%d is prime' % n)
else:
  self.response.write('%d is not prime' % n)
```
Change n to a couple different numbers. Notice that it never thinks a number is prime, even when it should. What's the problem here?

These kinds of bugs can be tricky to track down. Fortunately, logging can help you figure out exactly why it doesn't think any numbers are prime.

+ Add a logging statement in the for loop:

```python
for possible_factor in range(1, n):
  if n % possible_factor == 0:
    logging.info('Found a factor: %d', possible_factor)
    return False
```
Now try reloading the page with a different number. Check the logs: do you see the problem? How can you fix it?

#Conclusion

Patience young grasshopper. Debugging can be frustrating but you have tools that can help you fix errors in your code. Read your error messages in the console to find your next step. Use the PEP protocol. Ask for help!
