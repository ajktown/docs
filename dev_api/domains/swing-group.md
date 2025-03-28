# Domain hierarchy

<!-- TOC -->

- [Domain hierarchy](#domain-hierarchy)
  - [Overview](#overview)
  - [Prerequisites](#prerequisites)
    - [Measurer](#measurer)
  - [Here are the factors that indeed affect every single swing:](#here-are-the-factors-that-indeed-affect-every-single-swing)
    - [Your Body](#your-body)
    - [Weather](#weather)
    - [Where/How you swing?](#wherehow-you-swing)
    - [Your actual results of swings](#your-actual-results-of-swings)

<!-- /TOC -->

## Overview

Domain `SwingGroupDomain` contains fine-grained result of every shot (or group of shots). DB stores SwingGroupDomain as `swing-groups` table. But we do not store individual swing because it is too fine-grained. Instead, we store a group of swings as a `swing-group`. This domain is responsible for managing `swing-group` data.

## Prerequisites
### Measurer
Measurer matters because how you measure your muscle mass and flexibility really depends on what kind of machines you use, or what kind of ways to measure your flexibility. This is why every swing, there must be not only the factors, but also the measurer to standardize so that other factors do not confuse you.

## Here are the factors that indeed affect every single swing:

### Your Body
Your body indeed affects your swing. This includes:

- hours of sleep (can be a week, or can be a day, but it is up to you)
- weight
- muscle mass:
  - Arm
  - Leg
  - Core
- flexibility
- balance

Everything can be measured.


### Weather
Weather can affect your:
- mood
- actual results of your swing (balls)

And therefore it is important to measure the weather as well.
And of course, the measurer of the weather must be stay consistent by recommended, as if you start changing a lot, it will be less accurate for sure.

### Where/How you swing?
Your swing technique? Name it.
Your aim for the ball? Are you aiming the center of the ball? Or are you aiming the 9 oclock of the ball? What is your swing?
What kind of ground condition is it? Are you using? basic matts? 
What about the number of lane that youa re using in range? I mean why not record it even tho they won't affect so much!
How much are you doing the swing? of course your full shot and 3/4 shot will be different.

### Your actual results of swings
Again, measurer matters. what kind of software are you using? What version it is? Every software may result varies. You need to standardize the software as well as much as possible.