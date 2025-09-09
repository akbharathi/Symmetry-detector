<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

The symmetry detector checks if an 8-bit input is symmetric by comparing:
* Bit 0 with Bit 7
* Bit 1 with Bit 6
* Bit 2 with Bit 5
* Bit 3 with Bit 4

Key Components:
* XOR Gates: Compare symmetric bit pairs (output 1 if bits differ)
* AND Gates: Determine if all comparisons match (output 1 if symmetric)
* Mismatch Counter: Sums XOR outputs to count how many bit pairs differ

## How to test

The symmetry detector is tested using a Verilog testbench that applies various input patterns and verifies both the symmetry detection output and the mismatch count.

Key Test Cases Explained
* Example 1: Symmetric Pattern (8'b11000011)
Input: 1 1 0 0 0 0 1 1
Comparison pairs:
- Bit 0 (1) vs Bit 7 (1) → Match (XOR = 0)
- Bit 1 (1) vs Bit 6 (0) → Match (XOR = 0) 
- Bit 2 (0) vs Bit 5 (0) → Match (XOR = 0)
- Bit 3 (0) vs Bit 4 (0) → Match (XOR = 0)

Expected Output:
- out = 1 (symmetric)
- mismatch_count = 0

* Example 2: Asymmetric Pattern (8'b11010011)
Input: 1 1 0 1 0 0 1 1
Comparison pairs:
- Bit 0 (1) vs Bit 7 (1) → Match (XOR = 0)
- Bit 1 (1) vs Bit 6 (0) → Mismatch (XOR = 1)
- Bit 2 (0) vs Bit 5 (0) → Match (XOR = 0)
- Bit 3 (1) vs Bit 4 (0) → Mismatch (XOR = 1)

Expected Output:
- out = 0 (not symmetric)
- mismatch_count = 2 (two mismatched pairs)

## External hardware

LEDs used for outputs
