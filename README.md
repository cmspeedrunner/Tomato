![image](https://github.com/cmspeedrunner/Tomato/blob/29127156142e6b77a963e6b42a33d07c8da74013/Untitled.png)
# TomatoScript
TomatoScript is a dynamically typed programming language specialised in automating tasks with simple and concise syntax.
## Getting Started
Given you have both `interpreter.py` and `run.py` downloaded, make sure you also have `pyautogui` installed, this is the backbone for the automation scripts.<br>
## Syntax and Tutorial
TomatoScript *(being a pun on automation->automato->tomato)* is geared towards automating tasks, and has a bulk of the standard library dedicated to it, however, Tomato still features all the things you would expect from a programming language<br>
Lets start with printing. There are two ways in which you can print output, `println`, which adds a newline at the end of the value and `print`, which doesnt have a newline. For example:<br>
```python
println("Hello, ")
println("World!")
# This would output
# Hello, 
# World!

print("Hello, ")
print("World!")
# This would output
# Hello, World!
```
### Variable Assignment
Variable assignment is dynamic and simple, using the `let` keyword. Like this:
```python
let x = 10
let y = 10
let hello = "Hello"
let world = "World!"
println(x+y)
println(hello+", "+world)
```
You can also reassign types, like this:
```python
let x = "100"
println(int(x)+int(x))

# You can also do this:
let x = int(x)
println(x+x)
```

### Functions and Input
Functions are designated and opened with the `fn` keyword but need to be closed with the `end` keyword. For example:
```python
fn greet(name)
  println("Hello, "+name)
end

fn multiply(num1, num2)
  return num1*num2
end

greet("Mike")
greet("John")

println(multiply(5,5))
println(multiply(5.5, 5.5))
```
Input is easy to get using the `read` keyword. It is by default, stored as a string, but can be typecast to any value. For example:
```
let number = int(read("Enter a number>"))
println("Your number doubled is "+str(number*2))
let name = read("Enter your name>")
println("Hello, "+name)
```
### Control Flow
Else, Elif, If, While statements and for loops are opened with `then` and closed with `end`:
```python
let x = 20
let y = "20"

if x == y then
  println("Not possible!")
end
elif x == 20 then
  println("Possible!")
end
elif str(x) == y then
  println("Possible!"
else:
  println("You shouldn't get here")
```
## Scripting
The largest part of Tomato, is the automation scripting functionality. Here is a breakdown.
### Mouse
Mouse control is an expansive toolset which can be used, here is an example<br>
```python
mouseto(100,100) # Sends the mouse to the location specified.
mousefrom(50,50) # Adds the values relative to the mouse position, in this case +50 to both the x and y axis.
mousehold("left") # "left", "right" or "middle" are the options avalible. This holds the button until mouseup is called.
mouseup("left") # This releases the hold, mousehold and mouseto combined together create a drag function.
mouse("left") # This is the click function, it simply clicks the mouse button specified
mousescroll(200) # This scrolls the mouse by 200 units, a negative number will scroll down.

let x = getmousex() # Grabs the mouse current position on the x axis, allocating it into x
let y = getmousey() # Does the same for the Y axis
```
### Key
The key toolset is also expansive:
```python
key("a") # Presses and releases a single key.
keyhold("a") # Holds a single key until keyup is called.
keyup("a") # Releases the key
keyboard("Hello, World!", 0.01) # Autotypes the given value, the second argument decides the time interval, 0.0 is the quickest, but 0.01-0.001 minimum is reccomended.
hotkey("win", "r") # Allows for two keys to be held until a callback is recieved. Here we open up the run dialog.
```
### System and Flow toolsets
Here are some general system and flow tools:
```python
cmd("echo hello") # Passes a command to the command line
msg("Hello, World!") # Messages the user with a system message, can also be done through the cmd tool.
fopen("Hello.txt") # Open a file and read the content in one function.
fwrite("Hello, World!","Hello.txt") # Writes to a file, if the file doesnt exist, it is created.
wait(1) # Waits 1 second
let xbounds = getboundsx() # Gets the x resolution of the screen
let ybounds = getboundsy() # Gets the y resolution of the screen
wait(0.1) # Waits 100ms
println("Your resolution is "+str(xbounds)+"x"+str(ybounds) # Typecast the bounds values
browser("google.com") # Opens a browser tab, if a browser is already open, it will just open a tab in the existing session browser
```
### Importing a file as a library.
To import a .tmo file, you can use the `using` function. For example:
```python
using lib.tmo
dofunction()
```
### String manipulator
Tomato has a limited but still powerful string sanitisation toolkit.
```python
let untrimmed = "    hello     "
let trimmed = trim(untrimmed)
if trimmed == "hello" then
     msg("Trim works!")
end
```
There is also inbuilt regex:
```python
let string = "Tomato <<is the best>> programming language @@anyone agree??"
println(find(string, "<<" ">>"))
println(find(string, "@@","??"))
```
You can split strings:
```python
let string = "2+2"
let args = split(string, "+")
let num1 = args[0]
let num2 = args[1]
println(num1+num2)
```

### Other
You can format your code all in a single line using a semi-colon. Here is an example:
```python
 hotkey("win", "r"); wait(0.3); keyboard("notepad", 0.01); key("enter"); wait(0.75); keyboard("Hello, World!")
```
You can also define arrays and there is an inbuilt color system, but, i want to get to sleep , so, i'll leave you with a final example miniproject! It is a program which takes a refresh buffer (float type) input fromt he user, and then outputs the mouse coordinates infinitely.<br>
```python
fn outputBoundsMouse()
    
    println(col_blue+"You are "+col_green+str(getboundsx()-getmousex())+col_blue+"pxs away from the right side of your screen.")
    println("You are "+col_green+str(getmousex())+col_blue+"pxs away from the left side of your screen."+col_reset)
    println(col_purple+"-------------------------------"+col_blue)
    println("You are "+col_green+str(getboundsy()-getmousey())+col_blue+"pxs away from the bottom of your screen.")
    println("You are "+col_green+str(getmousey())+col_blue+"pxs away from the top of your screen."+col_reset)
end

let refresh = float(read("Enter refresh speed (seconds)"))

while True then
    outputBoundsMouse()
    wait(refresh)
    cmd("cls")
end
```

## Running the code
To run the code, invoke run.py like this:
`py run.py main.tmo`
You can also output the speed of the code by using the -s flag:
`py run.py main.tmo -s`
## Whats next?
I am going to continue to update the interpreter, add more scripting abillities, a website and hopefully a rewrite in c. Here is a full list of things I would like to do with this project.<br>
<ul>
  <li>Create GUI text editor/ide</li>
  <li>Create Website</li>
  <li>Rewrite in C</li>
  <li>Write shell interpreter</li>
</ul>
