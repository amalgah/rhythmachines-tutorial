# Tutorial

# Introduction

This is the first tutorial for rhythmachines, a new music sequencer within the sema environment. If you are unfamiliar with sema, it is a web based playground where you can rapidly prototype live coding mini-languages for signal synthesis, machine learning and machine listening.

It is recommended that if you have never used sema before, that you watch some introductory videos which can be found here.

[Introduction to Sema playlist](https://www.youtube.com/watch?v=RIAWj28tvxU&list=PLdzdpTgsHB7YrnDc3dflWYWgoHL4pmRPo&index=1 "Introduction to sema video playlist")

[Introduction to the default language](https://www.youtube.com/watch?v=RIAWj28tvxU "Introduction to the default language")


# Setting up the sequencing environment

Once you navigate to amalgah.github.io. Either login or continue as guest. To then set up the sequencer environment and a live-coding window you want to follow the following steps.

- Navigate to playground by using the navigation bar at the top of the page.
- Click reset on the left side pane to clear the environment.
- Select 3D Sequencer on the left side pane.
- Select the LiveCode Editor button on the left side pane. Using the dropdown menu then select default to use the default language.
- To start the audio engine click the speaker icon in the top right hand corner of the page.

You are now ready to start 3-Dimensional sequencing and live coding :)

# Controls

## Create a cylinder
- **Double Left Click** in a square on the grid.
	- A menu will pop up where you can enter values to create a cylinder with your desired specifications.

## Edit Cylinders Settings
- **Right Click** on a cylinder
  - A menu will appear where you can edit the cylinders speed or delete it.

## Create a Peg
- **Left Click** on any cylinder face.
  - This will create a peg at the location of the face.
  - The size of the peg is determined relative to the height and radius of the cylinder.

## Adjust Cylinder Rotation
- **Left Click** on a nudge button (the arrows above each cylinder).
  - This allows for phase control, by letting you slow down or speed up the rotation of a cylinder.


# Making a Sequence

Contrary to a traditional sequencer, the rhythmachines sequences are made with a combination of "cylinders" and "pegs" within a 3D environment.

Cylinders are the equivalent of a timeline in a traditional sequencer design. They can be any size and rotate when the sequencer is playing.

To then make a sequence, you can place pegs on the surface of a cylinder. Pegs act as sound triggers, when they touch another peg they send a signal on a designated audio channel. Similar to a channel you would get on a mixing desk.

Sema is a live-coding environment and so in order to receive signals from pegs in the live-coding window a special command must be used.

```
{0}fromSeq;
```

fromSeq indicates the name of the function, and within its parameters it has been passed a 0 which indicates the channel number. In this case, if a peg on channel 0 was to collide its signal would be returned from this function.


## Making Sound

One way you could use this to create sound is to pass the output of the fromSeq function into the `\` operator for sample playback.

```
>{{0}fromSeq}\909b;
```

If a peg on channel 0 were to make a collision with another peg, it would send its signal which would be received here and trigger a 909 bass sound to be played.

## Multiple Sounds

Usually you might want to have pegs on different channels so that they can trigger different sounds. To do this you will have to first right click the necassary pegs and enter different channel numbers.

To then receive trigger events from multiple pegs and hear them all together, you could do something like this:

```
:snare:{{0}fromSeq}\909;
:kick:{{1}fromSeq}\909b;
>{:snare:, :kick:}mix;
```

Here we have two variables `:snare:` and `:kick:` and mixing them together using the `mix` command.

There are 0 to 15 channels for you to use currently.



# Tips if things are not working

- Check that your code is compiling by navigating to Debuggers, then Live Code Parser Output. This will help you debug your code.
- Check that the audio engine is running (click the speaker icon in the top right).
- Sometimes things refuse to work properly, if all else fails reload the page and things should be working again.

# Useful code snippets

## Code for mixing multiple channels together
```
:a:{{0}fromSeq}\909;
:b:{{1}fromSeq}\909b;
:c:{{2}fromSeq}\909closed;
>{:a:, :b:, :c:}mix;
```
