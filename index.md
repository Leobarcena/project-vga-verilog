---
layout: home
title: FPGA VGA Driver Project
tags: fpga vga verilog
categories: demo
---

For this project I worked with an already made VGA design in Vivado. The original design showed different coloured stripes, and the goal was to modify it into something more detailed. I wanted to make my own image on the screen and actually control where each pixel goes. After I understood how the template worked, I added my own shapes to display a small scene with a ground, sky, tree and a cow that I created from coordinates.

### **Project Set-Up**
The project ran on an Artix-7 based FPGA connected to a VGA monitor. The screen resolution was 640×480, controlled by a VGA synchronization module. The given project already had:

- a VGA timing module

- a colour generator file

- a testbench

- device constraints

I programmed the FPGA through Vivado, connected the VGA cable to a monitor and verified the output.

Here is what the original display looked like before I edited anything:
I had forgotten to take a picture of my screen at the time I got the demo working. This picture I have demonstrated is from one of my class mates.
<img src="https://github.com/Leobarcena/project-vga-verilog/blob/main/docs/assets/images/20251111_140059.jpg">

### **Template Code**
The original template worked by checking the current row and col values of the pixel. Based on where the pixel was located, the code selected a colour. So any time a pixel fell inside a certain area, it would change to that assigned RGB value.
<img src="https://github.com/Leobarcena/project-vga-verilog/blob/main/docs/assets/images/image-1762871491130.jpg">

That is why the original screen just showed stripes — each stripe was simply controlled by:

`if(col >= X && col <= Y)`

At that stage nothing fancy was happening, just solid blocks of colour, but it gave me a good understanding of how the VGA mapping actually works.

### **Simulation**
I ran the behavioural simulation first to make sure everything was working before flashing the FPGA. In the simulator I could clearly see:

- hsync pulses happening across each row

- vsync changing once per full refresh

- col values counting up to 639

- row counting up to 479

And the RGB values changed exactly when the coordinates entered certain areas.
This already showed that the timing and colour selection was correct.

The waveform basically confirmed the whole pipeline before even touching the real hardware.

<img src="https://github.com/Leobarcena/project-vga-verilog/blob/main/docs/assets/images/20251202_135657.jpg">


### **Synthesis**
The design synthesized successfully. The warnings that appeared weren’t serious — mainly unused bits in the reset signals. Nothing affected the actual output.

Resource usage stayed very small, since most of the logic was comparisons and simple assignments. Timing also passed, meaning the design was running stable at VGA speed.

### **Demonstration**
After programming the FPGA, I connected it to a normal monitor and saw the stripes exactly as expected. The display was clean and stable and there was no flicker, so at that point I knew the template worked.

Here is what the original output looked like: 
<img src="https://github.com/Leobarcena/project-vga-verilog/blob/main/docs/assets/images/20251111_140059.jpg">

## **My VGA Design Edit**
## Design Overview

After testing the original version, I replaced the stripes with a more interesting scene. I created:

- a grassy ground
- a sky
- a tree (leaves + trunk)
- a yellow rectangle (sun) on the right
- and a pixel-style cow

I drew the cow on squared paper first so I could turn each square into coordinate ranges.
<img src="https://github.com/Leobarcena/project-vga-verilog/blob/main/docs/assets/images/20251125_153711.jpg">

I positioned everything based on the 640×480 grid. For example, the ground is basically:

 `if(col >= 11'd0 && col < 11'd640 && row >= 11'd340 && row < 11'd480) begin // green ground
      red_next   <= 4'b0000;
      green_next <= 4'b1111;
      blue_next  <= 4'b0000;
   end`

which colours the full area across the bottom.

### **Code Adaptation**
Instead of colouring full sections with vertical stripes, first thing I did was try to get some horizontal lines. 

Original code had the vertical lines like this: `col >= 200 && col < 320`
I added the horizontal lines by adding some extra lines. `row >= 180 && row < 260`
looked like this after it was done.`col >= 11'd0 && col < 11'd640 && row >= 11'd340 && row < 11'd480`

<img src="https://github.com/Leobarcena/project-vga-verilog/blob/main/docs/assets/images/20251111_140008.jpg">

Next step was to make a sky and ground, which was easier than the step above. 
Adding a tree and the sun were the next step after that.

stacking small rectangles. For example:
`col >= 200 && col < 320`
`row >= 180 && row < 260`
creates the top of the tree.
The same style of code but different coordinates made the trunk and sun.

<img src="https://github.com/Leobarcena/project-vga-verilog/blob/main/docs/assets/images/20251111_152622.jpg">

The cow was made with around 10 separate rectangles, all white, and positioned so they align to make a small cow shape. I basically highlighted small rectangular blocks and layered them so the face, chin and ears formed properly.

<img src="https://github.com/Leobarcena/project-vga-verilog/blob/main/docs/assets/images/Snapchat-676494236.jpg">

The important thing was to place all cow blocks above the default sky condition so the background wouldn’t overwrite them.

### **Simulation**
When I simulated my updated design, the RGB signals changed exactly where I expected. This confirmed that my coordinate values and conditions were correct and that the shapes would appear properly on hardware.

The overall timing and sync behaviour stayed the same, which means I didn’t break anything structurally.
### **Synthesis**
There was basically no difference in terms of resources. It is still just combinational comparisons, so Vivado handled it easily.
Warnings were the same as before and the design still met timing.
### **Demonstration**
Once I ran the bitstream to hardware again, the full scene appeared:

- ground at the bottom
- tree in the middle
- yellow block on the right
- cow drawn using rectangles

Everything lined up correctly and stayed displayed without flickering.
This confirmed that all my coordinate planning and code changes were correct.

<img src="https://github.com/Leobarcena/project-vga-verilog/blob/main/docs/assets/images/20251202_151748.jpg">

## Conclusion

Before modifying anything, I first understood how the VGA template worked. Then I took the same logic but used more detailed coordinate ranges so I could build shapes instead of stripes. Drawing the cow in my copybook first made placement much easier because I could visually plan the rectangles.

Overall, this helped me understand how VGA timing interacts with pixel positioning and how to make custom graphics manually. Seeing the design actually appear on the monitor was satisfying because I could directly see the result of the code I wrote.

## **More Markdown Basics**
This is a paragraph. Add an empty line to start a new paragraph.

Font can be emphasised as *Italic* or **Bold**.

Code can be highlighted by using `backticks`.

Hyperlinks look like this: [GitHub Help](https://help.github.com/).

A bullet list can be rendered as follows:
- vectors
- algorithms
- iterators

Images can be added by uploading them to the repository in a /docs/assets/images folder, and then rendering using HTML via githubusercontent.com as shown in the example below.

<img src="https://raw.githubusercontent.com/melgineer/fpga-vga-verilog/main/docs/assets/images/VGAPrjSrcs.png">
