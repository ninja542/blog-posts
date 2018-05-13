# Reflections for ideal gas

I told my teacher that this project would take longer than one month, and having a more relaxed deadline helped make me relax? This project definitely took a long time but I think I've gotten to the point where it's polished enough and I can move on from this project and use it for different projects.

This project definitely felt productive because I could branch this simulation off into heat-engine (next project), diffusion/effusion of two gases (rip I forgot the difference), and equilibrium/rates simulation. The last two simulations are more for chem, but I feel like a simulation would help a lot. 

## General thoughts/ramblings:

* I thought it was interesting that changing the volume changed the pressure, but not the temperature
* One small problem might be that increasing the number of particles increase the pressure, but not the temperature, which is what it's supposed to do.
* My Chem teacher really likes the sim
* The middle bit was the hardest (with trying to get collisions working), the last part was actually not that bad. The opposite usually happens, where the last part, the polishing, is the hardest. 
* I am excited that I know how to use the canvas (not like super well, but I kinda know it). I think it'll expand the functionality of future simulations that were previously limited by using only svg
* Animations are easier in Canvas, using canvas is very similar to using glowscript/vpython. 
* I learned Object Oriented Programming, which was interesting. I hope that I can learn functional programming next, although I don't think functional programming applies to the webapps/simulations that I'm doing right now.

I think that for the special relativity simulator I'll probably still use svg and not canvas animation, but rigged with vue logic so that it can be reactive. 

## Technical Details/Reflection

If you're reading this to gain some technical thoughts about the ideal gas simulation, I hope this helps. 

### Canvas

I used a pong game on canvas tutorial to help me begin with my simulation. This tutorial showed me how objects worked, how to use the canvas, how to animate the canvas and also gave me the wall collision code. (I promise the rest of the code I wrote).

I tried very hard to optimize the canvas early on, except I think I tried to optimize it way too early, because at that point, it was just a bunch of particles flying around without colliding with each other. I didn't really optimize the code for the collision checking and math, right now I don't see any better implementation because more efficient collision checking methods require much more overhead. So I just kept it like that. I know it's horribly inefficient, but since I limited the maximum number of particles, I think it'll be fine. 

I added a placeholder for collision code, which I felt that was smart because I could focus on other things. 

### Vue

Adding the Vue part to the code took a while because I didn't plan it out and I wasn't sure how vue and canvas animations were supposed to fit together. I think that I implemented Vue pretty well, it's very reactive and everything meshes together quite well. The update, animate, and render function is inside the vue function, but the step function is outside. 

### D3

I used D3 to show colorful particle tracking, which is still one of the best decisions I've made and I think that this is what sets it apart. 

To do this, I used the rainbow scale from d3.color, and scaled the particle velocity by dividing it by 8 (d3.color only accepts numbers between 0 and 1) and if the velocity was >8, it was automatically set at 1. A dynamic color system would've been way too confusing, so I just set the upper limit to 8 pixels/sec. 

I think it works pretty well for "normal temperatures", however if the gas is heated or cooled extremely, the particle tracking is less useful.

D3 was also used for the maxwell boltzmann distribution. I thought I could copy paste code from the graph in fountain simulator but it didn't work. Strangely, appending new svgs using d3 doesn't work after the vue object is closed. However, because of this, I discovered a more efficient way to draw and update graphs. 

Append an svg path (appending a class), Write a Vue method to update graph, Set a Vue watcher to dynamically update the graph. 

The last thing that I used d3 for was tracking the specific particle and plotting where it would be on the distribution graph. Used a similar system to the regular distribution graph, where the particle update also includes changing the rectangle height and position to fit onto the graph