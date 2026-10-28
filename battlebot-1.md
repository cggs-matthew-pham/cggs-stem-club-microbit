### @explicitHints true

# Battle Bot 1: Remote Control Robot

```template
let channel = ""
channel = "duck"
radio.setGroup(101)
basic.showIcon(IconNames.Duck)
```

## Introduction @showdialog
You've seen the soccer robot demo. Now you'll build it yourself.

You'll write **one program** and put it on **two** micro:bits:
- one plugs into your Move — the **robot**
- one you hold — the **remote**

The remote's buttons send messages. The robot listens and moves.

Stuck on a step? Click the **lightbulb** for a hint.

## Step 1: Group Number
In ``||radio:radio set group||``, change **101** to your **team's group number**.

#### ~ tutorialhint
Your teacher will help you pick a number nobody else in the room is using. Robots in different groups can't hear each other.

```blocks
radio.setGroup(101)
```

## Choose Your Robot's Icon @showdialog
Every robot shows an **icon**, so everyone can tell the robots apart. Pick one:

| Icon | Name |
|---|---|
| Duck | duck |
| Heart | heart |
| Ghost | ghost |
| Rabbit | rabbit |
| Giraffe | giraffe |
| Snake | snake |

Each team in your group needs a **different** icon. These six match the pictures on the Arcade controller later.

## Step 2: Show Your Icon
In ``||basic:show icon||``, choose **your** icon.

#### ~ tutorialhint
**Want your own icon?** Swap ``||basic:show icon||`` for ``||basic:show leds||`` and draw a 5×5 picture. Then make up a name for it in the next step (8 letters or fewer, no spaces).

```blocks
basic.showIcon(IconNames.Duck)
```

## Step 3: Your Robot's Name
In ``||variables:set channel to||``, type your icon's **name**, like **duck**.

#### ~ tutorialhint
Use small letters and spell it exactly. Your remote and robot must have the **same** name.

```blocks
let channel = ""
channel = "duck"
```

## Step 4: Team Colour
Open ``||Kitronik_Move_Motor:Move Motor||`` → **Lights**. Add ``||Kitronik_Move_Motor:set moveMotorZIP to MOVE Motor with 4 ZIP LEDs||`` and ``||Kitronik_Move_Motor:show color red||`` to the end of ``||basic:on start||``.

#### ~ tutorialhint
The lights on top of your Move show your **team**: **red** or **blue**. Your teacher will tell you which. You don't need to make the variable — the block comes with it.

```blocks
let channel = ""
channel = "duck"
radio.setGroup(101)
basic.showIcon(IconNames.Duck)
let moveMotorZIP = Kitronik_Move_Motor.createMoveMotorZIPLED(4)
moveMotorZIP.showColor(Kitronik_Move_Motor.colors(Kitronik_Move_Motor.ZipLedColors.Red))
```

## How a Message Works @showdialog
A radio message is like an **envelope**:
- On the **front** is a **name** — who it's for
- **Inside** is a **value** — a number for what to do

| Value | Move |
|---|---|
| 0 | Spin left |
| 1 | Spin right |
| 2 | Stop |
| 3 | Forward |
| 4 | Reverse |

So **duck** on the front with **3** inside means: *"duck, go forward!"*

Your robot will check the name, then read the number.

## Step 5: Receive a Message
From ``||radio:Radio||``, drag out ``||radio:on radio received name value||``.

#### ~ tutorialhint
This block runs every time an envelope arrives. It comes with ``||variables:name||`` (the front) and ``||variables:value||`` (inside).

```blocks
radio.onReceivedValue(function (name, value) {
})
```

## Step 6: Check the Name
Inside it, add ``||logic:if||`` ``||variables:name||`` **=** ``||variables:channel||``.

#### ~ tutorialhint
- Drag ``||variables:name||`` **off the top of the radio block**. Don't make a new variable.
- ``||variables:channel||`` is in ``||variables:Variables||`` — it's the name you chose in Step 3.

In plain words: *"Is this envelope for me?"*

```blocks
radio.onReceivedValue(function (name, value) {
    if (name == channel) {
    }
})
```

## Step 7: Forward
Inside the name check, add ``||logic:if||`` ``||variables:value||`` **= 3** → ``||Kitronik_Move_Motor:move Forward at speed 50||``.

#### ~ tutorialhint
Drag ``||variables:value||`` off the top of the radio block, like you did with ``||variables:name||``. It's the number inside the envelope.

```blocks
radio.onReceivedValue(function (name, value) {
    if (name == channel) {
        if (value == 3) {
            Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, 50)
        }
    }
})
```

## Step 8: Spin and Stop
Click **+** on that ``||logic:if||`` to add **else if** branches:
- **0** → ``||Kitronik_Move_Motor:spin Left at speed 20||``
- **2** → ``||Kitronik_Move_Motor:stop||``

#### ~ tutorialhint
Why no arrows on the screen? ``||basic:show arrow||`` takes half a second to draw, and the robot can't listen while it draws. A battle bot needs to be fast!

```blocks
radio.onReceivedValue(function (name, value) {
    if (name == channel) {
        if (value == 3) {
            Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, 50)
        } else if (value == 0) {
            Kitronik_Move_Motor.spin(Kitronik_Move_Motor.SpinDirections.Left, 20)
        } else if (value == 2) {
            Kitronik_Move_Motor.stop()
        }
    }
})
```

## Step 9: Teach It the Rest
Add two more **else if** branches:
- **1** → ``||Kitronik_Move_Motor:spin Right at speed 20||``
- **4** → ``||Kitronik_Move_Motor:move Reverse at speed 50||``

#### ~ tutorialhint
Your remote can only send three moves, but teach the robot all five anyway. You'll need them in Battle Bot 2!

```blocks
radio.onReceivedValue(function (name, value) {
    if (name == channel) {
        if (value == 3) {
            Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, 50)
        } else if (value == 0) {
            Kitronik_Move_Motor.spin(Kitronik_Move_Motor.SpinDirections.Left, 20)
        } else if (value == 2) {
            Kitronik_Move_Motor.stop()
        } else if (value == 1) {
            Kitronik_Move_Motor.spin(Kitronik_Move_Motor.SpinDirections.Right, 20)
        } else if (value == 4) {
            Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Reverse, 50)
        }
    }
})
```

## Now the Remote @showdialog
The robot part is done. Now the **remote**: making the envelopes.

``||radio:radio send value||`` has two spaces:
- **First:** the **name** on the front — use ``||variables:channel||``
- **Second:** the **value** inside — the move's number

When the robot gets it, these arrive as ``||variables:name||`` and ``||variables:value||``.

## Step 10: Button A Goes Forward
Add ``||input:on button A pressed||`` → ``||radio:radio send value||`` ``||variables:channel||`` **= 3**.

#### ~ tutorialhint
``||variables:channel||`` is in ``||variables:Variables||``. Drop it into the first space of the send block.

```blocks
input.onButtonPressed(Button.A, function () {
    radio.sendValue(channel, 3)
})
```

## Step 11: Spin and Stop Buttons
Add two more:
- ``||input:on button B pressed||`` → send **0** (spin left)
- ``||input:on button A+B pressed||`` → send **2** (stop)

#### ~ tutorialhint
Right-click your button A block and choose **Duplicate**, then change the button and the number.

```blocks
input.onButtonPressed(Button.A, function () {
    radio.sendValue(channel, 3)
})
input.onButtonPressed(Button.B, function () {
    radio.sendValue(channel, 0)
})
input.onButtonPressed(Button.AB, function () {
    radio.sendValue(channel, 2)
})
```

## Step 12: Download to Both
Download onto **both** micro:bits. Plug one into the Move and switch it on.

#### ~ tutorialhint
Same code on both. The remote ignores the motor blocks (no Move attached), and nobody presses the robot's buttons.

If nothing happens: check both show the same icon, and the same name is in ``||variables:set channel to||``.

## Step 13: Test Drive
Press **A** (forward), **B** (spin), **A+B** (stop).

#### ~ tutorialhint
The robot **keeps going** until you send the next move. Try driving to a target and stopping on it. What's tricky? Which moves do you wish you had?

## Complete! @showdialog
You've built a radio-controlled robot!

Remote and robot agree on what each number means. That's called a **protocol** — and it means you can swap in a whole new remote.

Next: drive it with an **Arcade controller** in **Battle Bot 2**:

https://arcade.makecode.com/#tutorial:github:cggs-matthew-pham/cggs-stem-club-arcade/battlebot-2-controller
