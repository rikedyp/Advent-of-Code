# AdventOfCode
My solutions to [Advent of Code](https://adventofcode.com/) problems.

Each folder becomes a namespace when the project is linked. Toolkit is in `#.kit`.

## Style
These solutions have been cleaned up and provided with additional commentary. When initially solving the problems, I experiment in the session until I get the correct answer as quickly as possible.

For example, for 2021 day 2, the line of code which provided my part 1 solution initially was:

```APL
      ×/{9 11∘.○((⍎⊃∘⌽)¨⍵)+.×1 0j1 0j¯1['fdu'⍳⊃¨⍵]}snl input2
1962940
```

This has been exploded out into the "waterfall" style of commentary:

```APL
 Day2_1←{
⍝ This solution uses complex numbers to represent 2-dimensional co-ordinates (horzontal position and depth)
     input←snl ⍵                                           ⍝ One instruction per line
     ×/9 11∘.○((⍎⊃∘⌽)¨input)+.×1 0J1 0J¯1['fdu'⍳⊃¨input]
⍝                                         'fdu'⍳⊃¨input    ⍝ forward, down or up?
⍝                              1 0J1 0J¯1[             ]   ⍝ 1 means +1 horizontal position
⍝                                                          ⍝ 0J1  is +1 depth
⍝                                                          ⍝ 0J¯1 is ¯1 depth
⍝             ((⍎⊃∘⌽)¨input)                               ⍝ X values (magnitudes) are the last character in each line
⍝                           +.×                            ⍝ Sum of magnitudes times directions
⍝      9 11∘.○                                             ⍝ Separate final co-ordinates
⍝    ×/                                                    ⍝ Multiply final co-ordinates
 }
```

## Workflow
1. Start Dyalog with the [configuration file](https://help.dyalog.com/latest/#UserGuide/Installation%20and%20Configuration/Configuration%20Files.htm) `aoc.dcfg`.

1. Go to this year's namespace and copy in the kit

```APL
      ⎕CS Y2022
      #.kit.Init⍕⎕THIS
```

## Getting input
Although I don't generally compete for the top spots in AoC, in theory it is important to import the input data as quickly as possible.

Before the new problem is released, log in to the [advent of code website](https://adventofcode.com).

Open the web developer tools.

> Press <kbd>F12</kbd> or <kbd><kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd> I </kbd> (on Firefox)

**Refresh** the page. **Right click** on the request and **copy** the request headers.

Paste them into the variable `headers` in the `#.kit` namespace.

You can then use the `pget` function from the kit:

```APL
      input6←pget 2021 6
```

## Parsing input
Now, the input is in the workspace as a simple character vector with embedded newline characters. So, the first step is usually to either split the input on newlines or 2-newlines.

For this I have the utilities `snl` (split new lines) and `sec` (section).