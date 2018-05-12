# Animation Studies
* DES132 - 3D Digital Literacy 2017/2018
* Niko Leskinen

## Research
For the research, I started reading The Animator's Survival Kit
written by Richard Williams.
The book provides principles and methods of animation that
Williams has learned through his career with other animators,
many of which have been creating Disney classic animations.

Many of the principles are just basic physics described in other words.
Timing, spacing, dragging and overlapping are just demonstrations
of inertia.
Although these  principles seem simple,
implementing them into animation was difficult.

For me the first useful lesson of the book was about key frames
and pose to pose animating method.
Drawing or animating key action or the static phases of action first
can be helpful. For example animating first phases of the walk where
weight is on the other foot and then filling in the other phases afterwards.

Williams talks also about relation of realism and believability.
How animations doesn't need to be realistic.
It only needs to seem like it is.
One example of this is Disney character Goofy's walk,
where foot goes sometimes backwards,
and joints are sometimes broken in completely unnatural way.
Yet the walk seems believable.




## Development
First I tried to animate this happy "The double bounce" walk and
I used The Animator's Survival Kit as a reference.
I am not complete satisfied about the result,
but at least I learned something about the rhythm of the cycle especially when
I tried to break the walking cycle by jump.

![The Double Bounce](https://github.com/lesenger/animationStudies/raw/master/bounce.png)


![TThe Happy Walk](https://github.com/lesenger/animationStudies/raw/master/happy.gif)

Next I tried to animate this cocky and arrogant walking style.
Inspiration was Oasis lead singer Liam Gallagher's walking style.
I used animated music video of the song Masterplan as a reference

[Oasis - The Masterplan](https://youtu.be/dPPi2D6GK7A?t=50s)


![Liam walk](https://github.com/lesenger/animationStudies/raw/master/liam.gif)

The rest two animations I made using python.
I wrote two scripts: The first one creates table/csv-file with object
attributes' values. Second one then reads the csv-file and runs maya
commands that saves keys attributes.
I got inspiration for this from Finnish author Linda Liukas
who writes books about programming and computers for children.
In the book main character Ruby has a recipe for dance
so I wanted to do similar thing with maya and walking.

[The poetry of programming Linda Liukas TEDxCERN](https://youtu.be/-jRREn6ifEQ?t=4m36s)

Program basically works in following way:
0. Give starting positions for walker's attributes.
1. Start repeating four phase as long as you want

![Walking cycle](https://github.com/lesenger/animationStudies/raw/master/walkCycleSketch.jpg)

First I used program to create relatively normal, maybe
little heavy walk.


![Normal Walk](https://github.com/lesenger/animationStudies/raw/master/normal.gif)


The second walk became partly by accident.
I forgot to change value for one variable and other leg didn't
move forward enough, and it looked little like wounded walk.
Then I changed rest of the walk cycle according this wound.


![Wounded Walk](https://github.com/lesenger/animationStudies/raw/master/wounded.gif

Python scripts I used are below.


## Application of Theory
At very first even basic walking sequence seemed hard,
but The Animator's Survival Kit gave helpful techniques
for the timing and poses.
The basic walk became then quite easy to animate.
However, this basic walk looks robotic and unnatural
without drag or overlapping effect.
This was also the hardest part of the animation.

## Outcomes
I am most satisfied with "the Liam walk". For me it looks like
most believable and little silly.
I got the dragging working for body and legs, but for some reason
when I tried it with foots, it didn't seem right.

I'm also pleased how the algorithm of walk turned out.
It took some time to write, but after that it was quite easy to
try different variations. Even changing value of one
variable could change walking style surprisingly much.

## Reflection
First thing I learned is that animation is lots of work.
I study theoretical computer science and mathematics and we are really
lazy. We try to do as little as possible and be compact and simple.
After that we give our work to computer and it will produce output.
Therefore animating was great opportunity to see the other approach
to working style.

I also started to observe how people on the street walked.
Now and then I also tried to mimic different walking style,
and I noticed that emotion of the walk affected to my mood.

I sure learned lot about animation and maya.
I probably would have learned more and maybe got better,
more believable outcome if I would have done
every animation by hand, but for me it was more interesting to
try to combine animation and programming.
And I hope I can use 3D animation program and programming
in the future, for example when I try to visualise something.


## Reflection of the module
This was really interesting module.
As a computer nerd it was exiting to collaborate with art people.
Certainly something that I wouldn't be able to do in my technical
home university.

I liked how both assignments were different. First more about modelling,
and second about animation.

At first, before attending any classes, I was a little uncertain
how this module is going to work out for me since
I cannot draw that well and I wasn't that familiar with creative process.
Although I think mathematics and programming is highly creative process,
but just in a different way.
But my fears ended up being unfounded.
Atmosphere in the class was always welcoming and these classes were
the ones I waited for.
I also liked teaching style, although I must say there was times
that I felt puzzled about what to do if the class was little unorganised.
This is mostly because I am used to that teaching starts on time and
is very structured and often strict.

All in all I enjoyed a lot and I have now greater interest towards animation.
At the same time I have now much better image of Belfast when I was
able to study at this campus.



## Python Code

### Script that creates the csv file

```python
import pandas as pd
import random
from copy import deepcopy
from recordclass import recordclass


Body = recordclass('Body', ['Frame', 'phase', 'tx', 'ty', 'tz', 'rx', 'ry', 'rz'])
Top = recordclass('Top', ['Frame', 'phase', 'ty'])
Leg = recordclass('Leg', ['Frame', 'phase', 'tx', 'ty', 'tz', 'rx', 'ry', 'rz',
                          'fr', 'fb', 'tr', 'lt', 'ht', 'bt', 'tt',
                          ])

State = recordclass('State', ['Frame', 'Body', 'Top', 'RightLeg', 'LeftLeg'])

df = pd.DataFrame(columns=['phase', 'b/tx', 'b/ty', 'b/tz', 'b/rx', 'b/ry', 'b/rz',
                           't/ty',
                           'lf/tx', 'lf/ty', 'lf/tz', 'lf/rx', 'lf/ry', 'lf/rz',
                           'lf/fr', 'lf/fb', 'lf/tr', 'lf/lt', 'lf/ht', 'lf/bt', 'lf/tt',
                           'rf/tx', 'rf/ty', 'rf/tz', 'rf/rx', 'rf/ry', 'rf/rz',
                           'rf/fr', 'rf/fb', 'rf/tr', 'rf/lt', 'rf/ht', 'rf/bt', 'rf/tt'])
df.index.name = 'Frame'
# Starting position
bStart = Body(Frame=0, phase=0, tx=0, ty=-0.25, tz=0, rx=0, ry=0, rz=0)
tStart = Top(Frame=0, phase=0, ty=0)
rfStart = Leg(Frame=0, phase=0, tx=0, ty=0,     tz=+1, rx=0, ry=0, rz=0, fr=0, fb=0, tr=0, lt=0, ht=0, bt=0, tt=0)
lfStart = Leg(Frame=0, phase=0, tx=0, ty=0,     tz=-1, rx=0, ry=0, rz=0, fr=0, fb=0, tr=0, lt=0, ht=0, bt=0, tt=0)

states = []
states.append(State(bStart.Frame, bStart, tStart, rfStart, lfStart))

def writeStateToDataFrame(state):
    frame = state.Frame
    # Body
    B = state.Body
    df.at[B.Frame, 'phase'] = B.phase
    df.at[B.Frame, 'b/tx'] = B.tx
    df.at[B.Frame, 'b/ty'] = B.ty
    df.at[B.Frame, 'b/tz'] = B.tz
    df.at[B.Frame, 'b/rx'] = B.rx
    df.at[B.Frame, 'b/ry'] = B.ry
    df.at[B.Frame, 'b/rz'] = B.rz
    # Top
    T = state.Top
    df.at[T.Frame, 't/ty'] = T.ty
    # RightLeg
    R = state.RightLeg
    df.at[R.Frame, 'rf/tx'] = R.tx
    df.at[R.Frame, 'rf/ty'] = R.ty
    df.at[R.Frame, 'rf/tz'] = R.tz
    df.at[R.Frame, 'rf/rx'] = R.rx
    df.at[R.Frame, 'rf/ry'] = R.ry
    df.at[R.Frame, 'rf/rz'] = R.rz

    df.at[R.Frame, 'rf/fr'] = R.fr
    df.at[R.Frame, 'rf/fb'] = R.fb
    df.at[R.Frame, 'rf/tr'] = R.tr
    df.at[R.Frame, 'rf/lt'] = R.lt
    df.at[R.Frame, 'rf/ht'] = R.ht
    df.at[R.Frame, 'rf/bt'] = R.bt
    df.at[R.Frame, 'rf/tt'] = R.tt

    # LeftLeg
    L = state.LeftLeg
    df.at[L.Frame, 'lf/tx'] = L.tx
    df.at[L.Frame, 'lf/ty'] = L.ty
    df.at[L.Frame, 'lf/tz'] = L.tz
    df.at[L.Frame, 'lf/rx'] = L.rx
    df.at[L.Frame, 'lf/ry'] = L.ry
    df.at[L.Frame, 'lf/rz'] = L.rz

    df.at[L.Frame, 'lf/fr'] = L.fr
    df.at[L.Frame, 'lf/fb'] = L.fb
    df.at[L.Frame, 'lf/tr'] = L.tr
    df.at[L.Frame, 'lf/lt'] = L.lt
    df.at[L.Frame, 'lf/ht'] = L.ht
    df.at[L.Frame, 'lf/bt'] = L.bt
    df.at[L.Frame, 'lf/tt'] = L.tt

print(df)
FRAMESTEP = 8
FORWARD_ON_PHASE = 1


def moveTop(state, refState):
    ROUNDNESS = 0.2

    frameShift = +3
    refPhase = refState.Top.phase
    state.Top.phase = (refPhase + 1) % 4
    state.Top.Frame = state.Frame + frameShift

    if refPhase == 0:
        state.Top.ty = 0
    elif refPhase == 1:
        state.Top.ty = - ROUNDNESS *0.9
    elif refPhase == 2:
        state.Top.ty = + ROUNDNESS*0.2
    elif refPhase == 3:
        state.Top.ty = - ROUNDNESS*0.5


def moveBody(state, refState):
    frameShift = 0
    UP_POS = -0.25
    DOWN_POS = -0.6
    HOR_ROTATION = 25
    DOWN_ROTATION = 10

    refPhase = refState.Body.phase
    state.Body.phase = (refPhase + 1) % 4
    state.Body.Frame = state.Frame + frameShift

    if refPhase == 0:
        state.Body.tz -= FORWARD_ON_PHASE
        state.Body.ty = UP_POS
        state.Body.ry = 0
        state.Body.rz = 0
    elif refPhase == 1:
        state.Body.tz -= FORWARD_ON_PHASE
        state.Body.ty = DOWN_POS
        state.Body.ry = - HOR_ROTATION
        state.Body.rz = + DOWN_ROTATION
    elif refPhase == 2:
        state.Body.tz -= FORWARD_ON_PHASE *0.5
        state.Body.ty = UP_POS
        state.Body.ry = 0
        state.Body.rz = 0
    elif refPhase == 3:
        state.Body.tz -= FORWARD_ON_PHASE *0.5
        state.Body.ty = DOWN_POS + 0.4
        state.Body.ry = + HOR_ROTATION
        state.Body.rz = - DOWN_ROTATION






def moveRightLeg(state, refState):
    frameShift = 0
    refPhase = refState.RightLeg.phase
    state.RightLeg.phase = (refPhase + 1) % 4
    state.RightLeg.Frame = state.Frame + frameShift

    if refPhase == 0:
        pass
    elif refPhase == 1:
        state.RightLeg.fr = 30
        state.RightLeg.fb = 30
        state.RightLeg.ty = 0
    elif refPhase == 2:
        state.RightLeg.fr = 20
        state.RightLeg.fb = 0
        state.RightLeg.tz = -state.Body.tz-1.5
        state.RightLeg.ty = 0.05
    elif refPhase == 3:
        state.RightLeg.tz = -state.Body.tz + FORWARD_ON_PHASE*0.7
        state.RightLeg.fr = 0
        state.RightLeg.fb = 0
        state.RightLeg.ty = 0



def moveLeftLeg(state, refState):
    frameShift = 0
    refPhase = refState.LeftLeg.phase
    state.LeftLeg.phase = (refPhase + 1) % 4
    state.LeftLeg.Frame = state.Frame + frameShift

    if refPhase == 0:
        state.LeftLeg.fr = 40
        state.LeftLeg.fb = 0
        state.LeftLeg.tz = -state.Body.tz-1
        state.LeftLeg.ty = 0.2
    elif refPhase == 1:
        state.LeftLeg.tz = -state.Body.tz + FORWARD_ON_PHASE * 0.5
        state.LeftLeg.fr = 0
        state.LeftLeg.fb = 0
        state.LeftLeg.ty = 0
    elif refPhase == 2:
        pass
    elif refPhase == 3:
        state.LeftLeg.fr = 30
        state.LeftLeg.fb = 30




def nextState(refState):
    frameStep = FRAMESTEP
    newState = deepcopy(refState)
    newState.Frame = refState.Frame + frameStep
    moveBody(newState, refState)
    moveTop(newState, refState)
    moveRightLeg(newState, refState)
    moveLeftLeg(newState, refState)
    return newState

refState = states[-1]
for i in range(40):
    newState = nextState(refState)
    states.append(newState)
    refState = states[-1]

for state in states:
    writeStateToDataFrame(state)

df.to_csv('algorithmOfWalkFourPhases.csv', sep=';')

print(df)

```

### Script that reads the csv file and tuns maya commands

``` python
import pandas as pd
import numpy
from re import match
import maya.cmds as cmds



def run():
    D = {'b': 'CTRL_Main',
         't': 'CTRL_Top',
         'lf': 'walker_lf_heel_ik_ctrl',
         'rf': 'walker_rt_heel_ik_ctrl',
         'tz': 'translateZ',
         'ty': 'translateY',
         'tx': 'translateX',
         'rx': 'rotateX',
         'ry': 'rotateY',
         'rz': 'rotateZ',
         'fr': 'footRoll',
         'fb': 'footBreak',
         'tr': 'toeRoll',
         'lt': 'legTwist',
         'ht': 'heelTwist',
         'bt': 'ballTwist',
         'tt': 'toeTwist',
         }
    kneeL = 'walker_lf_knee_pv_ctrl'
    kneeR = 'walker_rt_knee_pv_ctrl'
    cmds.cutKey(D['b'], time=(0,1000))
    cmds.cutKey(D['t'], time=(0, 1000))
    cmds.cutKey(D['lf'], time=(0,1000))
    cmds.cutKey(D['rf'], time=(0,1000))


    def key(frame, obj, atr, value):
        cmds.setKeyframe(obj, at=atr, v=value, t=frame)
        print('{} {} {} {}'.format(obj, atr, value, frame))


    key(0, kneeL, D['tz'], 1000)
    key(0, kneeR, D['tz'], 1000)


    walk_df = pd.read_csv("algorithmOfWalkFourPhases.csv", sep=';').set_index("Frame")


    def regind(expression):
        return [column[0] for column in enumerate(walk_df) if match(expression, column[1])]


    print(walk_df)

    for frame, row in walk_df.iterrows():
        for atrib, value in row.iteritems():
            if not numpy.isnan(value):
                print("Frame:", int(frame), atrib, value)
                m = match(r"(\w+)/(\w+)",atrib)
                if m and m.group(2):
                    if m.group(2) in D:
                        object = m.group(1)
                        atribute = m.group(2)
                        print(object)
                        print(atribute)
                        print(D[object],D[atribute])
                        key(frame,D[object],D[atribute],value)
```
