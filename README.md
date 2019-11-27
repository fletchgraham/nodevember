# Nodevember 2019

This repository contains my solutions to the prompts for Nodevember, a yearly event focused on exploring procedural node-based workflows. That means that everything is 100% procedural with no help from image textures. I'll add related explorations in the extras folder. @ or dm me on twitter if you have questions!

**Scroll down to day 03 to see a breakdown of my lightning shader.**

Thus far, all of my work on this project is made with [Blender](https://www.blender.org/). 

## Day 23: Planet

![](/img/23-planet-1.jpg)

## Day 14: Ornamental

![](/img/14-ornate-2.jpg)

## Day 10: Flower

![10-flower-1](/img/10-flower-1.jpg)

## Day 05: Snow

![05-snow-2](/img/05-snow-2.png)

## Day 04: Tornado

![04-tornado-1](/img/04-tornado-1.png)

## Day 03: Lightning

![](/img/03-lightning-1.png)

The image above shows a simple 2D plane with my lightning shader applied. Two objects can be specified in the shader and it will draw arcs of lightning between the two objects. 

### Breakdown/ Tutorial

#### 1. Connect Point A to Point B

My first task was to figure out something seemingly simple: how to draw a line from point A to point B using Blender's shader nodes. 

![connect-pints-1](/img/03-lightning-2.png)

My strategy was to make a set of nodes that would draw a line on the Y axis in any given object space, then **rotate the entire object space to get it to "look at" another point.** 

Here's what my node group for rotating a vector looks like:

![03-lightning-6](/img/03-lightning-6.png)

I got the node recipe for vector rotation from this [helpful article](https://medium.com/@behreajj/coding-blender-materials-with-nodes-python-66d950c0bc02). 

 After obtaining a new object space with its origin at point A and its "up" direction aimed at point B, connecting the points is as simple as drawing a line on the Y axis within that rotated space. The length that the line should be is obtained with the help of ol' Pythagoras.

I believe the setup of two connected points would be a useful starting point for many different use cases, so I've included the blend file in the extras folder. 

#### 2. Segments and branching

Breaking the line into segments and translating the connecting points results in some zig-zag. Overdrawing the connecting lines creates the branching effect.

![03-lightning-3](/img/03-lightning-3.png)

In the above setup, I've grouped the nodes responsible for aiming and drawing the lines so that they they can be reused to draw multiple lines. A mix RGB node is used to find the middle point between A and B, then an arbitrary vector is added to to move it away from dead middle. 

To create the branch, the length socket for that line is intercepted by a simple Add node.

#### 3. Distortion

![03-lightning-04](/img/03-lightning-04.png)

My tactic for distorting the lines was to mix in a noise texture to the object space of each of the target objects. 

Noise generates values from zero to one, but the lightning should be able to wiggle in all directions so 0.5 is substracted from each channel. Then, to increase the effect of noise, each channel can be multiplied by some value.

#### 4. Glow

The last step is to use the resulting output as a mix factor for a transparent and emissive shader.

![03-lightning-5](/img/03-lightning-5.png)

#### 5. Experiment

There's a blend file with this simple lightning setup in the extras folder

Stuff to try:

* Break up the line into more segments. My final lightning has 8 segments.
* Make the branches less intense than the main arc.
* Add multiple arcs of lightning with slightly different parameters.
* Try animating different parameters.

## Day 02: Clouds

![02-clouds-1](/img/02-clouds-1.png)


## Day 01: Lava

![](/img/01-lava-1.png)

