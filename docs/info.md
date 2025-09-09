<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

Compare mirrored bits with XOR:

xor x1(w[0], i[0], i[7]);
xor x2(w[1], i[1], i[6]);
xor x3(w[2], i[2], i[5]);
xor x4(w[3], i[3], i[4]);


Each XOR compares the first half of the input with the mirrored second half.

w[0] = 1 if i[0] ≠ i[7], otherwise 0.

Similarly, w[1], w[2], w[3] for other pairs.

Generate intermediate AND signals:

and a1(w[4], ~w[0], ~w[1]);
and a2(w[5], ~w[2], ~w[3]);


Checks if first pair and second pair both match (~w = 1 if bits match).

Final output:

and a3(out, w[4], w[5]);


out = 1 only if all mirrored bit pairs match → input is symmetric.

Count mismatches:

assign mismatch_count = w[0] + w[1] + w[2] + w[3];


Adds up mismatched pairs.

Example: if only i[0] ≠ i[7] and i[2] ≠ i[5], mismatch_count = 2.

## How to test

Create a testbench module
Simulation checks:
out should be 1 only for symmetric inputs.

mismatch_count should match the number of differing mirrored bit pairs.

Example:

Input=10011001 → Out=1, Mismatch=0
Input=10101011 → Out=0, Mismatch=3

## External hardware

LEDs used for outputs
