# Exercise: Control your Duckiebot {#exercise-control type=slides status=ready nonumber=1}


Goal: Apply a control strategy to make a Duckiebot drive in a lane.  

Requires: A calibrated (camera and odometry) and charged Duckiebot in configuration `DB18`, a laptop and an internet connection.

Recommended: Basic knowledge of Algebra and Control Theory.

Results: Your own implementation of a controller.



## Preliminaries: Getting the math right

A simple model for a Duckiebot could be:

<figure class="stretch">
  <img style='width:6em'  src="model.png"/>
</figure>

State:

$$
x = [ d,\phi ]^T
$$

Input:

$$
u=\omega
$$

Dynamics:

$$
\begin{bmatrix} \dot{d}=v_0\cdot \sin(\phi)\\ \dot{\phi}=\omega=u \end{bmatrix}
$$

The LTI system:
$$
\dot{x}=\begin{bmatrix}
 0& v_0 \\
0 & 0
\end{bmatrix}x+ \begin{bmatrix}
  0\\
  1
\end{bmatrix} u,\quad y=\begin{bmatrix}
1 & 0 \\
0 & 1
\end{bmatrix}x
$$

## Derivation of a PI controller

Augment states with integrals:

$$
z=[d,\phi,d_I,\phi_I]^T
$$

Augmented system:

$$
\dot{z}=\begin{bmatrix}
 A & 0_{2\times2} \\
I_{2\times2} & 0_{2\times2}
\end{bmatrix}z+ \begin{bmatrix}
  B\\
  0_{2\times1}
\end{bmatrix} u,\quad y_n=I_{4\times4}z
$$

We close the loop with:

$$
u = -K\cdot y_n \quad where \quad K= [k_{P_d},k_{P_\phi},k_{I_d},k_{I_\phi}
$$


## Our beloved pipeline


<figure class="stretch">
  <img style='width:30em'  src="loop.png"/>
</figure>

For this exercise, we will use a different controller rather than the standard one used in the `lane_controller_node`.


## Controller template

<figure class="stretch">
  <img style='width:30em'  src="controller.png"/>
</figure>

You can edit the file with any editor you like?



## How to launch your own controller

*On your Duckiebot*
First you will need to run the docker image created for this exercise.

Note: Make sure your ros-picam and joystick containers are off.

```markdown
run the controller
```
Once this is running,
```markdown
ssh and navigate
```

Then launch the controller
```markdown
roslaunch stuff
```

*On your laptop*
Run the keyboard control, enter autonomous mode pressing `a`, stop it with `s`.

## References
