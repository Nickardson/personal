+++
title = "Teaching Kids Python with Tracy the Turtle"
subtitle = "Impressing kids can be a good strategy."
summary = "Impressing kids can be a good strategy."
date = 2019-01-10T00:00:00Z
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["taylor"]

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["python"]
categories = []

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["deep-learning"]` references 
#   `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
# projects = ["internal-project"]

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
[image]
  # Caption (optional)
  caption = ""

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""
+++

At CentralSquare, we regularly host an _Hour of Code_ where middle-school students learn programming and share their creations with their classmates. Code.org has a lot of lessons available, but [Tracy the Turtle](https://codehs.com/hourofcode/tracy) allows some freedom and teaches an actual language using Python and Turtle graphics.

When we get to the part where the kids can make whatever they want, we found that giving the kids some inspiration and a starting point helped them to show off their code more. Having something to show off speaks more to the power of code than simply solving pre-made problems; like the difference between something made in art class vs. an equation solved in math class.

So we kick off the creativity by demonstrating some simple code effects which the students can remix. (The following programs were written by a colleague.)

[Go the final step of the lesson to try these samples.](https://codehs.com/editor/hoc/1072564/6642/4751)

### Star Spiral

{{< split_preview >}}
{{< figure src="sample-1.png" class="m-0" >}} ||

```python
colors=["red","orange","yellow","green","blue","purple"]
speed(0)
bgcolor("black")
for x in range(300):
    color(colors[x % 6])
    forward(x * .5)
    left(100)
    forward(x * .5)
    right(160)
```

{{</ split_preview >}}

### Hypnotic Spiral

{{< split_preview >}}
{{< figure src="sample-2.png" class="m-0" >}} ||

```python
colors=["red","orange","yellow","green","blue","purple"]
speed(0)
bgcolor("black")
for x in range(1200):
    color(colors[x%6])
    forward(x*.5)
    left(149)
```

{{</ split_preview >}}

### Ring Spiral

{{< split_preview >}}
{{< figure src="sample-3.jpg" class="m-0" >}} ||

```python
speed(0)
bgcolor('black')

colors=['red','purple','blue','green','orange','yellow']

def drawCircles(size):
    for i in range (10):
        circle(size)
        size=size-4
        color(colors[i%6])
def drawSpecial(size,repeat):
  for i in range (repeat):
    drawCircles(size)
    right(360/repeat)
drawSpecial(100,10)
```

{{</ split_preview >}}

### Snowflake Spiral

{{< split_preview >}}
{{< figure src="sample-4.png" class="m-0" >}} ||

```python
colors=["red","white","blue"]

def draw_edge(s):
    forward(s)
    right(90)

def draw_square(s):
    begin_fill()
    for i in range(4):
        draw_edge(s)
    end_fill()

speed(0)

penup()
setposition(-200,200)
pendown()
color("black")
begin_fill()
draw_square(400)
end_fill()
penup()
setposition(0,0)
pendown()

for x in range(100):
    circle(x)
    color(colors[x%3])
    left(60)
```

{{</ split_preview >}}

## Tracy Tricks

You can do anything you like with a Python program running on your PC. But there's something that seems more legitimate about showing the code running on the actual Code.org site. Showing how the sausage is made shows the kids... you can also make your own sausage.

But once you start trying to go past the suggested behavior covered in the tutorials, you run into some challenges. There are a few things I discovered while pushing the limits of the embedded [Skulpt](https://skulpt.org/) Python-in-JavaScript engine.

### Ludicrous Speed

You can use `speed()` to make things render faster, to a certain point.

```python
# Actions run faster
speed(10)

# Actions run with no animation. Instant... right? Not exactly.
speed(0)
```

But complex or dynamic drawings take too long. Using `tracer()` skips rendering between a certain number of actions.

```python
# 40 actions are performed before the next draw
import turtle
turtle.tracer(40, 0)
# Note that nothing is drawn until 40 actions are performed.
# You can manually draw at any point.
turtle.update()
```

I made a [fork of Spiral Betty](https://github.com/Nickardson/spiral-betty) by Shalanah Dawson to output a python-compatible array of coordinates which draws a spiral. This would take too long to draw normally.

{{< split >}}
{{< figure src="sample-6.png" link="https://gist.github.com/Nickardson/778d1d940284eb31fc4cf93cffba526d" class="m-0" >}} ||
{{< figure src="sample-7.png" link="https://gist.github.com/Nickardson/5600db7439ee6aef6ce66fa46c135e24" class="m-0" >}} ||
{{< figure src="sample-5.png" link="https://gist.github.com/Nickardson/e596d745cb714bdbd40be587fdee67c7" class="m-0" >}}
{{</ split >}}

```python
import turtle
# It seems almost like cheating, but there is about 300kb of data drawing the Fortnite image.
# This is only part of the spiral data. Click on the images above.
spiral = [[0.3,0.1,1.8],[0.5,0.2,1.81],[0.6,0.5,1.81], ...]
turtle.tracer(40, 0)

bgcolor((1, 252, 255))
color((5, 64, 122))
penup()
for point in spiral:
    pensize(point[2])
    setposition(point[0] * 0.5, point[1] * 0.5)
    pendown()
```

## Games, Keyboard Interaction, and Multiple Turtles

1. `screen.onkey(func, "Up")` runs a function on keyboard interaction.
1. `screen.ontimer(func, intervalMs)` runs a function on a fixed game loop.
1. `turtle.Turtle()` creates additional turtles which can be independently controlled.

{{< figure src="sample-snake.gif" width="50%" class="m-0" >}}

```python
import turtle
import random
turtle.tracer(1000, 0) # ultra speed

screen = turtle.Screen()

# we want a snake!
snake = screen.turtles()[0]
snake.color("green")
snake.penup()

# and a fruit
fruit = turtle.Turtle()
fruit.color("red")
fruit.shape("circle")
fruit.penup()

segments = 1 # how many segments is our snake, and how fast?
trail = [] # where have we been?

def game_loop():
  global segments

  snake.forward(20) # move forward

  # if we hit ourselves, game over!
  if (any(snake.distance(p[0]) < 1 for p in trail)):
    segments = 1
    snake.setposition(0, 0)
    bgcolor((random.random()*128+127, random.random()*128+127, random.random()*128+127))

  # remember the trail
  trail.append((snake.pos(), snake.heading()))
  while (len(trail) > segments):
    trail.pop(0)

  # draw the snake
  snake.clear()
  for location in trail:
    snake.setposition(location[0])
    snake.setheading(location[1])
    snake.stamp()
  
  # eat the fruit if we hit it
  if (snake.distance(fruit.pos()) < 20):
    fruit.setposition(random.randint(-9, 9) * 20, random.randint(-9, 9) * 20)
    segments += 2

  turtle.update()
  screen.ontimer(game_loop, 1000 / (segments / 10 + 5))

# controls
def up():
  snake.setheading(90)
def right():
  snake.setheading(0)
def down():
  snake.setheading(270)
def left():
  snake.setheading(180)

screen.onkey(up, "Up")
screen.onkey(right, "Right")
screen.onkey(down, "Down")
screen.onkey(left, "Left")
screen.listen()

game_loop()
```
