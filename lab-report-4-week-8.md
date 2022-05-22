[Return to Index Page](https://andrewonozuka.github.io/cse15l-lab-reports/index)

[Link to Lab Report 4 Writeup](https://docs.google.com/document/d/1q7HzkBHREFiAFCbs5-SdMA8vxfdkV2vxAqGMB-haE5U/edit?usp=sharing)

# Lab Report 4 | Week 8

## Background

In this lab report, we compare our implementation of markdown parser with another group. Below are the links to the two repositories and the three snippets that will be relevant in our comparisons.

*Snippet #1*
```
`[a link`](url.com)

[another link](`google.com)`

[`cod[e`](google.com)

[`code]`](ucsd.edu)
```

*Snippet #2*
```
[a [nested link](a.com)](b.com)

[a nested parenthesized url](a.com(()))

[some escaped \[ brackets \]](example.com)
```

*Snippet #3*
```
[this title text is really long and takes up more than 
one line

and has some line breaks](
    https://www.twitter.com
)

[this title text is really long and takes up more than 
one line](
https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule
)


[this link doesn't have a closing parenthesis](github.com

And there's still some more text after that.

[this link doesn't have a closing parenthesis for a while](https://cse.ucsd.edu/



)

And then there's more text
```

## Expected Outputs

Snippet #1: [url.com, google.com, ucsd.edu]
Snippet #2: [b.com, example.com]
Snippet #3: [https://www.twitter.com, https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule]

## Turning Snippets into Tests

![](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screen%20Shot%202022-05-22%20at%2014.44.15.png?raw=true)

## Our Implementation

Did not pass.

![]()

## Review Implementation

Did not pass.

![](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/ss-lr4/Screen%20Shot%202022-05-22%20at%2014.47.47.png?raw=true)


For the implementation you reviewed in Week 7, the corresponding output when running the tests; if it passed, say so. If it didn’t pass, show the specific part of the JUnit output that shows the test failure.

## Questions

Do you think there is a small (<10 lines) code change that will make your program work for snippet 1 and all related cases that use inline code with backticks? If yes, describe the code change. If not, describe why it would be a more involved change.


Do you think there is a small (<10 lines) code change that will make your program work for snippet 2 and all related cases that nest parentheses, brackets, and escaped brackets? If yes, describe the code change. If not, describe why it would be a more involved change.
Do you think there is a small (<10 lines) code change that will make your program work for snippet 3 and all related cases that have newlines in brackets and parentheses? If yes, describe the code change. If not, describe why it would be a more involved change.
If your code already works on some/all test cases, include an explanation of what were the code changes that allowed the tests to pass.
