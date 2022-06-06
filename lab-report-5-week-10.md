[Return to Index Page](https://andrewonozuka.github.io/cse15l-lab-reports/index)

[Link to Lab Report 5 Writeup](https://docs.google.com/document/d/1SDw_yH2dxa5G4i6Vewm_5wglgdgoVNY-o8AtrPuPQmc/edit#)

# Lab Report 5 | Week 10

## Finding Differences Between Two Text Files

I found the tests with different results using the following command:

```
vimdiff my-markdown-parser/results.txt markdown-parser/results.txt
```

As we can see in the picture below, we can see which tests produced different results.

![](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/ss-lr5/Screen%20Shot%202022-06-05%20at%2023.33.37.png?raw=true)

I decided to take a look at files 201 and 342.

## Link to Test Files

[Test 201](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/201.md)

[Test 342](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/342.md)

## Determining Correct Output

Test 201:

There are no valid links. The correct output should simply be [].

Test 342:

There are no valid links. The correct output should simply be [].

## Each Implementation

my-markdown-parser:

This is a correct implementation, as we get both outputs at [].

![](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/ss-lr5/Screen%20Shot%202022-06-05%20at%2023.52.02.png?raw=true)

markdown-parser:

This is not a correct implementation, as we do not get []. In order to fix this, we would need to be able to check if the section inside the parenthesis has a valid url (for example check if there is a common prefix or suffix).

![](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/ss-lr5/Screen%20Shot%202022-06-05%20at%2023.50.46.png?raw=true)


