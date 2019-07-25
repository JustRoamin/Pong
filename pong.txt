#   Creator: Joshua M. Haddix
#   Created: 7/18/2019
#   Updated: 7/18/2019
#   Description: Pong to be used for future AI projects

import turtle

window = turtle.Screen()
window.title("Pong")
window.bgcolor("black")
window.setup(width=800, height=600)
window.tracer(0)

# Score
score1 = 0
score2 = 0

# Paddle 1
paddle1 = turtle.Turtle()
paddle1.speed(0)
paddle1.shape("square")
paddle1.color("White")
paddle1.shapesize(stretch_wid=5, stretch_len=1)
paddle1.penup()
paddle1.goto(-350, 0)

# Paddle 2
paddle2 = turtle.Turtle()
paddle2.speed(0)
paddle2.shape("square")
paddle2.color("White")
paddle2.shapesize(stretch_wid=5, stretch_len=1)
paddle2.penup()
paddle2.goto(350, 0)

# Ball
ball = turtle.Turtle()
ball.speed(0)
ball.shape("square")
ball.color("White")
ball.penup()
ball.goto(0, 0)
ball.dx = .4
ball.dy = .4

# Pen
pen = turtle.Turtle()
pen.speed(0)
pen.color("white")
pen.penup()
pen.hideturtle()
pen.goto(0,260)
pen.write("P1: 0          P2: 0", align ="center", font=("Courier", 12, "normal"))


# Function
def paddle1_up():
    y = paddle1.ycor()
    y += 30
    paddle1.sety(y)

def paddle1_down():
    y = paddle1.ycor()
    y -= 30
    paddle1.sety(y)

def paddle2_up():
    y = paddle2.ycor()
    y += 30
    paddle2.sety(y)

def paddle2_down():
    y = paddle2.ycor()
    y -= 30
    paddle2.sety(y)

# Hotkey
window.listen()
window.onkeypress(paddle1_up, "w")
window.onkeypress(paddle1_down, "s")
window.onkeypress(paddle2_up, "Up")
window.onkeypress(paddle2_down, "Down")

# Main game loop
while True:
    window.update()

    # ball movement
    ball.setx(ball.xcor() + ball.dx)
    ball.sety(ball.ycor() + ball.dy)

    # ball borders
    if ball.ycor() > 290:
        ball.sety(290)
        ball.dy *= -1

    if ball.ycor() < -290:
        ball.sety(-290)
        ball.dy *= -1

    if ball.xcor() > 390:
        ball.goto(0,0)
        ball.dx *= -1
        score1 += 1
        pen.clear()
        pen.write("P1: {}          P2: {}".format(score1, score2), align ="center", font=("Courier", 12, "normal"))

    if ball.xcor() < -390:
        ball.goto(0,0)
        ball.dx *= -1
        score2 += 1
        pen.clear()
        pen.write("P1: {}          P2: {}".format(score1, score2), align ="center", font=("Courier", 12, "normal"))

    # paddle borders
    if (paddle1.ycor() > 250):
        paddle1.sety(250)

    if (paddle1.ycor() < -250):
        paddle1.sety(-250)

    if (paddle2.ycor() > 250):
        paddle2.sety(250)

    if (paddle2.ycor() < -250):
        paddle2.sety(-250)


    # Collisions - Cor() is based off the center of the object so we need + / - comparisons for each side of the paddle
    if (ball.xcor() > 340 and ball.xcor() < 350) and (ball.ycor() < paddle2.ycor() + 52 and (ball.ycor() > paddle2.ycor() - 52)):
        ball.setx(340)
        ball.dx *= -1

    if (ball.xcor() < -340 and ball.xcor() > -350 ) and (ball.ycor() < paddle1.ycor() + 52 and (ball.ycor() > paddle1.ycor() - 52)):
        ball.setx(-340)
        ball.dx *= -1