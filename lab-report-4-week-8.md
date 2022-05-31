[Return to Index Page](https://andrewonozuka.github.io/cse15l-lab-reports/index)

[Link to Lab Report 4 Writeup](https://docs.google.com/document/d/1q7HzkBHREFiAFCbs5-SdMA8vxfdkV2vxAqGMB-haE5U/edit?usp=sharing)

# Lab Report 4 | Week 8

## Background

In this lab report, we compare our implementation of markdown parser with another group. Below are the links to the two repositories and the three snippets that will be relevant in our comparisons.

[Our Implementation](https://github.com/andrewonozuka/markdown-parser)

[Review Implementation](https://github.com/HantianLin/markdown-parser)

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

## Expected Outputs Using VS Code Preview

Snippet #1:

![](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/ss-lr4/Screen%20Shot%202022-05-31%20at%2000.04.58.png?raw=true)

Snippet #2:

![](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/ss-lr4/Screen%20Shot%202022-05-31%20at%2000.05.28.png?raw=true)

Snippet #3: 

![](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/ss-lr4/Screen%20Shot%202022-05-31%20at%2000.05.40.png?raw=true)

## Turning Snippets into Tests

![](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/ss-lr4/Screen%20Shot%202022-05-22%20at%2014.44.15.png?raw=true)

**Our Implementation**

Did not pass.

![](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/ss-lr4/Screen%20Shot%202022-05-22%20at%2014.52.47.png?raw=true)

**Review Implementation**

Did not pass.

![](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/ss-lr4/Screen%20Shot%202022-05-22%20at%2014.47.47.png?raw=true)

## Questions

**Snippet 1**

Do you think there is a small (<10 lines) code change that will make your program work for snippet 1 and all related cases that use inline code with backticks? If yes, describe the code change. If not, describe why it would be a more involved change.

Our Code:

Yes. We can check to see if there are any backticks within the parenthesis to see if the link is invalid or not. This would solve the fact that we were getting the correct outputs except for "`google.com".

Review Code:

Yes. The other group can check to see if there are any backticks within the parenthesis to see if the link is invalid or not. This would solve the fact that we were getting the correct outputs except for "`google.com".

**Snippet 2**

Do you think there is a small (<10 lines) code change that will make your program work for snippet 2 and all related cases that nest parentheses, brackets, and escaped brackets? If yes, describe the code change. If not, describe why it would be a more involved change.

Our Code:

No. While it wouldn't be too difficult to fix the index out of bounds error, it is much harder to see which parenthesis should be used/ignored within the intended parenthesis.

Review Code:

No. It is difficult to determine which parenthesis should be prioritized and which should be ignored with in "(a.com(()))" within 10 lines of code.

**Snippet 3**

Do you think there is a small (<10 lines) code change that will make your program work for snippet 3 and all related cases that have newlines in brackets and parentheses? If yes, describe the code change. If not, describe why it would be a more involved change.

Our Code:

Yes. Our code did well in ignoring the majority of the latter chunk, however we still need to make sure that not everything is ignored, since our output was []. We should still get the first two links despite them having line breaks, so it should look like ["https://www.twitter.com","https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule"].

Review Code:

No. The code ignores the first link but returns everything else (inluding the unwanted buffer text). It would take longer than 10 lines.