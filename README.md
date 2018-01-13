# Canvas-3D-Renderer
With this program, I'll be trying to learn and understand 3D geometry and camera perspectives on canvas.

## Introduction
I'm game developer and i use some 3D tools everyday. But as a programmer and physics student, i'm not familar with 3D geometry and perspective calculations. In this repository, i'll be trying to understand and learn 3D geometry and camera perspectives. I'll be working with 2D Canvas context on HTML5 scheme.

To understand code, you have to be familar with 2D canvas and JavaScript.

### Subjects : 
+ 3D Geometry (Position, rotation and camera)
+ Light Physics or raytracing (For graphical part)
+ Raycasting and some basic physic calculations in 3D world
+ Optimizing

# 3D Geometry

## Drawing points on HTML Canvas
First of all, i'll draw my model's points on canvas with calculating their positions. I'll calculate these positions from a matrix. And future models will be calculated with same method. Array contains 3 dimensions of a point. A simple point should be like that :
```
[0,0,0]
```

So simple box model should be like that :
```
[-1,-1,-1],
[ 1,-1,-1],
[ 1, 1,-1],
[-1, 1,-1],
[ 1, 1, 1],
[-1, 1, 1],
[-1,-1, 1],
[ 1,-1, 1]
```

They are points of an box object. A simple cube has 8 point and 6 faces. We'll merge faces on calculation function so points will be enough on our wireframe drawings.

Note : In my first design, i was using 0 instead of -1. But it ended up with origin problem. And i've changed them to -1 to centerize my object.

## Fundamentals of 3D perspective
Modern games mostly uses perspective projection camera systems. So in my project, i'll be working with projection perspective. I'm not sure about that but i think ortographic and perspective camera calculations are different.

With some little Google research i found this formula :
```
x' = x * fov / (z + viewer_distance) + half_screen_width
y' = -y * fov / (z + viewer_distance) + half_screen_height
(no z) 
```

This formula calculates x and y positions of a point on 2D surface. Because of that, there is no Z dimension. So i have to calculate all position information with this snippet.

That function calculates 2D position of a point. But we have to calculate it's rotation and position information as well. And sum up all of these values to find exact position of point.

We have 3 different rotation calculations and they are :

### Rotating Along X :
```
y' = y*cos(a) - z*sin(a)
z' = y*sin(a) + z*cos(a)
x' = x
```

### Rotating Along Y :
```
z' = z*cos(a) - x*sin(a)
x' = z*sin(a) + x*cos(a)
y' = y
```

### Rotating Along Z :
```
x' = x*cos(a) - y*sin(a)
y' = x*sin(a) + y*cos(a)
z' = z
```

I found these informations from that gist : https://gist.github.com/xem/99930986c5333125a13b0ea50600391f

We are done with this position and rotation calculations. You can find them in index.html file, these calculations are used in calculatePoint and calculateRotation functions. I'll optimize them later. Currently i'm done with 3D perspective and geometry.

Here is result from geometry and 3D perspective calculations :

![Screen01](http://imagets.com/shared/canvas-renderer/screen01.jpg)

Also here is link from current state :
http://imagets.com/shared/canvas-renderer/level01.html

I put some range sliders to see different perspectives. I'll also put camera movement in future, for now these basic sliders are enough.

Last Update : 01/14/2018