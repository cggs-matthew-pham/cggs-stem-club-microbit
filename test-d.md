### @explicitHints true

# Battle Bot 1: Remote Control Robot

```package
radio
pxt-kitronik-move-motor=github:kitronikltd/pxt-kitronik-move-motor#v0.4.20
```

```template
let REVERSE = 0
let FORWARD = 0
let STOP = 0
let SPIN_RIGHT = 0
let SPIN_LEFT = 0
let channel = ""
channel = "duck"
radio.setGroup(101)
SPIN_LEFT = 0
SPIN_RIGHT = 1
STOP = 2
FORWARD = 3
REVERSE = 4
basic.showIcon(IconNames.Duck)
```

## How a Message Works @showdialog
A radio message is like an **envelope**:
- On the **front** is a **name** — who it's for
- **Inside** is a **value** — a number for what to do

| Value | Name in your code |
|---|---|
| 0 | SPIN_LEFT |
| 1 | SPIN_RIGHT |
| 2 | STOP |
| 3 | FORWARD |
| 4 | REVERSE |

So **duck** on the front with **3** inside means: *"duck, go forward!"*

You don't have to remember the numbers. Your code already has a **name** for each one, like ``||variables:FORWARD||`` = 3. Use the names, and the code reads like English.

Your robot will check the name, then read the number.

## Step 5: Receive a Message
From ``||radio:Radio||``, drag out ``||radio:on radio received name value||``.

#### ~ tutorialhint
This block runs every time an envelope arrives. It comes with ``||variables:name||`` (the front) and ``||variables:value||`` (inside).

```blocks
radio.onReceivedValue(function (name, value) {
})
```

## Step 6: Add an If
Inside ``||radio:on radio received||``, add an ``||logic:if then||`` block.

#### ~ tutorialhint
The robot is about to ask a question: *"Is this envelope for me?"* An ``||logic:if||`` block asks a question.

```blocks
radio.onReceivedValue(function (name, value) {
    if (true) {
    }
})
```

## Step 7: Add a Comparison
From ``||logic:Logic||``, drag the **text** comparison ``||logic:"" = ""||`` into the ``||logic:if||``, replacing **true**.

#### ~ tutorialhint
Make sure it's the one with **quotes** (`" "`), not the one with **0**. Names are words, not numbers, so we need the text one.

```blocks
radio.onReceivedValue(function (name, value) {
    if ("" == "") {
    }
})
```

## Step 8: The Name on the Envelope
Drag ``||variables:name||`` **off the top of the radio block** into the **left** side of the comparison.

#### ~ tutorialhint
Click and drag the little ``||variables:name||`` at the top of ``||radio:on radio received||``. Don't make a new variable — this one holds the name on the envelope that just arrived.

```blocks
radio.onReceivedValue(function (name, value) {
    if (name == "") {
    }
})
```

## Step 9: Check It's You
From ``||variables:Variables||``, drag ``||variables:channel||`` into the **right** side.

#### ~ tutorialhint
``||variables:channel||`` is the name **you** chose in Step 3. Now the robot asks: *"Is this envelope's name **my** name?"* If not, it ignores the message.

```blocks
radio.onReceivedValue(function (name, value) {
    if (name == channel) {
    }
})
```

## Step 10: Check the Number
Inside the name check, add another ``||logic:if||`` with the **number** comparison ``||logic:0 = 0||``. Drag ``||variables:value||`` off the radio block into the left, and ``||variables:FORWARD||`` from ``||variables:Variables||`` into the right.

#### ~ tutorialhint
This time it's the comparison with **0** — the value inside is a **number**. ``||variables:FORWARD||`` is just a name for **3**, set up for you in ``||basic:on start||``.

```blocks
radio.onReceivedValue(function (name, value) {
    if (name == channel) {
        if (value == FORWARD) {
        }
    }
})
```

## Step 11: Forward
Inside ``||logic:if value = FORWARD||``, add ``||Kitronik_Move_Motor:move Forward at speed 50||``.

#### ~ tutorialhint
The envelope said ``||variables:FORWARD||``, so the robot drives!

```blocks
radio.onReceivedValue(function (name, value) {
    if (name == channel) {
        if (value == FORWARD) {
            Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, 50)
        }
    }
})
```

## Step 12: Stop for Anything Else
Click **+** once on the ``||logic:if value = FORWARD||`` block. It adds an **else**. Put ``||Kitronik_Move_Motor:stop||`` inside it.

#### ~ tutorialhint
**else** means *"for any other number"*. So ``||variables:STOP||`` stops the robot — and so does any number it doesn't know. That's a safe default!

Why no arrows on the screen? ``||basic:show arrow||`` takes half a second to draw, and the robot can't listen while it draws.

```blocks
radio.onReceivedValue(function (name, value) {
    if (name == channel) {
        if (value == FORWARD) {
            Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, 50)
        } else {
            Kitronik_Move_Motor.stop()
        }
    }
})
```

## Step 13: Spin Left
Click **+** again. This adds an **else if** above the else. Make it ``||variables:value||`` **=** ``||variables:SPIN_LEFT||`` → ``||Kitronik_Move_Motor:spin Left at speed 20||``.

#### ~ tutorialhint
New **else if** branches always appear **above** the else. That's fine — the else stays last, catching everything else.

```blocks
radio.onReceivedValue(function (name, value) {
    if (name == channel) {
        if (value == FORWARD) {
            Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, 50)
        } else if (value == SPIN_LEFT) {
            Kitronik_Move_Motor.spin(Kitronik_Move_Motor.SpinDirections.Left, 20)
        } else {
            Kitronik_Move_Motor.stop()
        }
    }
})
```

## Step 14: Teach It the Rest
Click **+** twice more for two more **else if** branches:
- ``||variables:SPIN_RIGHT||`` → ``||Kitronik_Move_Motor:spin Right at speed 20||``
- ``||variables:REVERSE||`` → ``||Kitronik_Move_Motor:move Reverse at speed 50||``

#### ~ tutorialhint
Your remote can only send three moves, but teach the robot all five anyway. You'll need them in Battle Bot 2!

```blocks
radio.onReceivedValue(function (name, value) {
    if (name == channel) {
        if (value == FORWARD) {
            Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, 50)
        } else if (value == SPIN_LEFT) {
            Kitronik_Move_Motor.spin(Kitronik_Move_Motor.SpinDirections.Left, 20)
        } else if (value == SPIN_RIGHT) {
            Kitronik_Move_Motor.spin(Kitronik_Move_Motor.SpinDirections.Right, 20)
        } else if (value == REVERSE) {
            Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Reverse, 50)
        } else {
            Kitronik_Move_Motor.stop()
        }
    }
})
```

## Now the Remote @showdialog
The robot part is done. Now the **remote**: making the envelopes.

``||radio:radio send value||`` has two spaces:
- **First:** the **name** on the front — use ``||variables:channel||``
- **Second:** the **value** inside — the move, like ``||variables:FORWARD||``

When the robot gets it, these arrive as ``||variables:name||`` and ``||variables:value||``.

## Step 15: Button A Goes Forward
Add ``||input:on button A pressed||`` → ``||radio:radio send value||`` ``||variables:channel||`` **=** ``||variables:FORWARD||``.

#### ~ tutorialhint
``||variables:channel||`` and ``||variables:FORWARD||`` are both in ``||variables:Variables||``.

```blocks
input.onButtonPressed(Button.A, function () {
    radio.sendValue(channel, FORWARD)
})
```

## Step 16: Spin and Stop Buttons
Add two more:
- ``||input:on button B pressed||`` → send ``||variables:SPIN_LEFT||``
- ``||input:on button A+B pressed||`` → send ``||variables:STOP||``

#### ~ tutorialhint
Right-click your button A block and choose **Duplicate**, then change the button and the move.

```blocks
input.onButtonPressed(Button.A, function () {
    radio.sendValue(channel, FORWARD)
})
input.onButtonPressed(Button.B, function () {
    radio.sendValue(channel, SPIN_LEFT)
})
input.onButtonPressed(Button.AB, function () {
    radio.sendValue(channel, STOP)
})
```

## Step 17: Download to Both
Download onto **both** micro:bits. Plug one into the Move and switch it on.

#### ~ tutorialhint
Same code on both. The remote ignores the motor blocks (no Move attached), and nobody presses the robot's buttons.

If nothing happens: check both show the same icon, and the same name is in ``||variables:set channel to||``.

## Step 18: Test Drive
Press **A** (forward), **B** (spin), **A+B** (stop).

#### ~ tutorialhint
The robot **keeps going** until you send the next move. Try driving to a target and stopping on it. What's tricky? Which moves do you wish you had?

## Complete! @showdialog
You've built a radio-controlled robot!

Remote and robot agree on what each number means. That's called a **protocol** — and it means you can swap in a whole new remote.

Next: drive it with an **Arcade controller** in **Battle Bot 2**:

https://arcade.makecode.com/#tutorial:github:cggs-matthew-pham/cggs-stem-club-arcade/battlebot-2-arcade-controller
