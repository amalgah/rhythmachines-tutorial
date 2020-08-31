# Introduction to the RHYTHMACHINES Sequencer.

This is the first tutorial for a new music sequencer within the sema environment. If you are unfamiliar with sema, it is a web based playground where you can rapidly prototype live coding mini-languages for signal synthesis, machine learning and machine listening.

It is recommended that if you have never used sema before, that you watch some introductory videos which can be found here.

## Introduction to sema video playlist
https://www.youtube.com/watch?v=RIAWj28tvxU&list=PLdzdpTgsHB7YrnDc3dflWYWgoHL4pmRPo&index=2


## Introduction to the default language
https://www.youtube.com/watch?v=RIAWj28tvxU (Particularly useful information about the default language used in sema is covered in this video).



# Making a Sequence

Contrary to a traditional sequencer, the rhythmachines sequences are made with a combination of "cylinders" and "pegs" within a 3D environment.

Cylinders are the equivalent of a timeline in a traditional sequencer design. They can be any size and rotate when the sequencer is playing.

To then make a sequence, you can place pegs on the surface of a cylinder. Pegs act as sound triggers, when they touch another peg they send a signal on a designated audio channel. Similar to a channel you would get on a mixing desk.

Sema is a livecoding environment and so in order to recieve signals from pegs in the livecoding window a special command must be used.

```
{0}fromSeq;
```

fromSeq indicates the name of the function, and within its parameters it has been passed a 0 which indicates the channel number. In this case, if a peg on channel 0 was to collide its signal would be returned from this function.

One way you could use this to create sound is to pass the output of the fromSeq function into the `\` operator for sample playback.

```
>{{0}fromSeq}\909b;
```

If a peg on channel 0 were to make a collision with another peg, it would send its signal which would be received here and trigger a 909 bass sound to be played.


# Controls

## Create a cylinder
- **Double L-Click** in a square on the grid.
	- A menu will pop up where you can enter values to create a cylinder with your desired specifications.

## Edit Cylinders Settings
- **Right Click** on a cylinder
  - A menu will appear where you can edit the cylinders speed or delete it.

## Create a Peg
**Left Click** on any cylinder face.
  - This will create a peg at the location of the face.
  - The size of the peg is determined relative to the height and radius of the cylinder.



# Some useful examples

## Code for mixing multiple channels together
```
:a:{{0}fromSeq}\909;
:b:{{1}fromSeq}\909b;
:c:{{2}fromSeq}\909closed;
>{:a:, :b:, :c:}mix;
```

## Creating a melody
One way you could create a melody is by setting different signal values for multiple pegs and have them trigger a saw wave.
