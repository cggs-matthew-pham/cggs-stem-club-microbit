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
let moveMotorZIP = Kitronik_Move_Motor.createMoveMotorZIPLED(4)
moveMotorZIP.showColor(Kitronik_Move_Motor.colors(Kitronik_Move_Motor.ZipLedColors.Red))
```

