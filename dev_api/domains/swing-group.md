# Domain hierarchy

<!-- TOC -->

- [Domain hierarchy](#domain-hierarchy)
  - [Overview](#overview)
  - [Prerequisites](#prerequisites)
    - [Measurer](#measurer)
  - [Here are the factors that indeed affect every single swing:](#here-are-the-factors-that-indeed-affect-every-single-swing)
    - [Your Body](#your-body)
    - [Before swing, what have you done?](#before-swing-what-have-you-done)
    - [Weather](#weather)
    - [WIth Who?](#with-who)
    - [Your equipment?](#your-equipment)
    - [Where/How you swing?](#wherehow-you-swing)
    - [Your actual results of swings](#your-actual-results-of-swings)

<!-- /TOC -->

## Overview

TODO: It would be awesome if this model can apply for all:
- actual course swing
- actual putter swing
- actual chip shot
- actual bunker shot
- actual driver swing
- actual iron swing
- practice swing
- pracitce grene swing
- practice in range
- practice with coach

TODO: It would be awesome to train the machine learning model to apply all the test!

 TODO: It would be awesome to have al lthe version model so that we are not losing any data!

Domain `SwingGroupDomain` contains fine-grained result of every shot (or group of shots). DB stores SwingGroupDomain as `swing-groups` table. But we do not store individual swing because it is too fine-grained. Instead, we store a group of swings as a `swing-group`. This domain is responsible for managing `swing-group` data.

## Prerequisites
### Measurer
Measurer matters because how you measure your muscle mass and flexibility really depends on what kind of machines you use, or what kind of ways to measure your flexibility. This is why every swing, there must be not only the factors, but also the measurer to standardize so that other factors do not confuse you.

## Here are the factors that indeed affect every single swing:

### Your Body
Your body indeed affects your swing. This includes:

- weight- hours of sleep (can be a week, or can be a day, but it is up to you)

- muscle mass:
  - Arm
  - Leg
  - Core
- flexibility
- balance

And your mood? maybe you can use apple watch to measure your heart rate, and see how your heart rate affects your swing.
Did you go to gym yesterday? when was the last time you did physical activities? These matter a lot.

How many hours of drives/ orjust getting ride before swinging? 
What kind of food did you have last 24 hours?
DId you go to bathroom before swinging?
How many water did you drink before swinging?

Everything can be measured.


### Before swing, what have you done?


### Weather
Weather can affect your:
- mood
- actual results of your swing (balls)

- how humid
- how hot (temperature)
- wind
- rain/snow
- how bright it is?

And therefore it is important to measure the weather as well.
And of course, the measurer of the weather must be stay consistent by recommended, as if you start changing a lot, it will be less accurate for sure.

Time? By default the time will be saved automaticall,y but you can customize and add later too. but it is recommended to add as you've done the swing.

### WIth Who?
How loud is it?
What kind of people are around you?
If you are practicing with your coach, your enemy? or your girlfriend that you want to show off your swing?
These factors matter a lot.


### Your equipment?
Not only your club number or anything, we need your:
- club weight
- club length
- club grip
- club head
- club shaft
- club flex
- club brand
- club model
- club year
- club condition
- club grip condition

And your:
- shoes
- spikes
- gloves
- hat
- glasses, are you wearing sunglasses/ What model?


### Where/How you swing?
Your swing technique? Name it.
Your aim for the ball? Are you aiming the center of the ball? Or are you aiming the 9 oclock of the ball? What is your swing?
What kind of ground condition is it? Are you using? basic matts?
What about the number of lane that youa re using in range? I mean why not record it even tho they won't affect so much!
How much are you doing the swing? of course your full shot and 3/4 shot will be different.

- your toe angle?
- your grip angle?


Are you swinging on green? (putterin?)
are you swinging on bunker? stuff?

- are you using second floor ? first floor?
- how wide you are opening
- where is the club placed at before swing
- how much you are bending your knees
- how much you are bending your waist

### Your actual results of swings
Again, measurer matters. what kind of software are you using? What version it is? Every software may result varies. You need to standardize the software as well as much as possible.