---
layout: home
title: FPGA VGA Driver Project
tags: fpga vga verilog
categories: demo
---

For this project I worked with an already made VGA design in Vivado. The original design showed different coloured stripes, and the goal was to modify it into something more detailed. I wanted to make my own image on the screen and actually control where each pixel goes. After I understood how the template worked, I added my own shapes to display a small scene with a ground, sky, tree and a cow that I created from coordinates.

### **Project Set-Up**
The project ran on an Artix-7 based FPGA connected to a VGA monitor. The screen resolution was 640×480, controlled by a VGA synchronization module. The given project already had:

a VGA timing module

a colour generator file

a testbench

device constraints

I programmed the FPGA through Vivado, connected the VGA cable to a monitor and verified the output.

Here is what the original display looked like before I edited anything:
<img src="https://github.com/Leobarcena/project-vga-verilog/blob/main/docs/assets/images/20251111_140059.jpg">

### **Template Code**
The original template worked by checking the current row and col values of the pixel. Based on where the pixel was located, the code selected a colour. So any time a pixel fell inside a certain area, it would change to that assigned RGB value.

if(col > X && col < Y && row > A && row < B)

<img src="https://github.com/Leobarcena/project-vga-verilog/docs/assets/images
/image-1762871491130.jpg">

At that stage nothing crazy was happening, just solid blocks of colour, but it gave me a good understanding of how the VGA mapping actually works.

That is why the original screen just showed stripes — each stripe was simply controlled by:
### **Simulation**
Explain the simulation process. Reference any important details, include a well-selected screenshot of the simulation. Guideline: 1/2 short paragraphs.
### **Synthesis**
Describe the synthesis and implementation processes. Consider including 1/2 useful screenshot(s). Guideline: 1/2 short paragraphs.
### **Demonstration**
Perhaps add a picture of your demo. Guideline: 1/2 sentences.

## **My VGA Design Edit**
Introduce your own design idea. Consider how complex/achievabble this might be or otherwise. Reference any research you do online (use hyperlinks).
### **Code Adaptation**
Briefly show how you changed the template code to display a different image. Demonstrate your understanding. Guideline: 1-2 short paragraphs.
### **Simulation**
Show how you simulated your own design. Are there any things to note? Demonstrate your understanding. Add a screenshot. Guideline: 1-2 short paragraphs.
### **Synthesis**
Describe the synthesis & implementation outputs for your design, are there any differences to that of the original design? Guideline 1-2 short paragraphs.
### **Demonstration**
If you get your own design working on the Basys3 board, take a picture! Guideline: 1-2 sentences.

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
