
[Return to Index Page](https://andrewonozuka.github.io/cse15l-lab-reports/index)

# Lab Report 2 | Week 4 | Fixing Markdown Parser

## Background

In the lab for week 3, we took a look at MarkdownParse.java, which looks something like this:

```
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;

public class MarkdownParse {

    public static ArrayList<String> getLinks(String markdown) {
        ArrayList<String> toReturn = new ArrayList<>();
        // find the next [, then find the ], then find the (, then read link upto next )
        int currentIndex = 0;
        while(currentIndex < markdown.length()) {
            int openBracket = markdown.indexOf("[", currentIndex);
            int closeBracket = markdown.indexOf("]", openBracket);
            int openParen = markdown.indexOf("(", closeBracket);
            int closeParen = markdown.indexOf(")", openParen);
            toReturn.add(markdown.substring(openParen + 1, closeParen));
            currentIndex = closeParen + 1;
        }
        return toReturn;
    }

    public static void main(String[] args) throws IOException {
        Path fileName = Path.of(args[0]);
        String content = Files.readString(fileName);
        ArrayList<String> links = getLinks(content);
	    System.out.println(links);
    }
}
```

The program is intended to find the links given in a certain "---.md" file and return an ArrayList of links.

Through labs 3 and 4, our goal is to focus on **incremental development**, which our programming process is driven by tests. This allows us to catch mistakes early and often, therefore avoiding situations where you have a large program with many errors that you do not know the source of.

## Code Change #1

Screenshot of code change diff from Github:

![Screenshot](https://github.com/andrewonozuka/markdown-parser/blob/main/Screen%20Shot%202022-04-24%20at%2005.22.21.png?raw=true)

[Failure Inducing Input #1](https://github.com/andrewonozuka/markdown-parser/edit/main/test-file.md)


Show the symptom of that failure-inducing input by showing the output of running the file at the command line for the version where it was failing (this should also be in the commit message history)

[Failing Output #1](https://github.com/andrewonozuka/markdown-parser/edit/main/test-file.md)

[Passing Output #1](https://github.com/andrewonozuka/markdown-parser/edit/main/test-file.md)

Write 2-3 sentences describing the relationship between the bug, the symptom, and the failure-inducing input.

## Code Change #2

Show a screenshot of the code change diff from Github (a page like this)

![Screenshot](https://github.com/andrewonozuka/markdown-parser/blob/main/Screen%20Shot%202022-04-24%20at%2005.22.21.png?raw=true)

Link to the test file for a failure-inducing input that prompted you to make that change


Show the symptom of that failure-inducing input by showing the output of running the file at the command line for the version where it was failing (this should also be in the commit message history)


Write 2-3 sentences describing the relationship between the bug, the symptom, and the failure-inducing input.

## Code Change #3

Show a screenshot of the code change diff from Github (a page like this)

![Screenshot](https://github.com/andrewonozuka/markdown-parser/blob/main/Screen%20Shot%202022-04-24%20at%2005.22.21.png?raw=true)

Link to the test file for a failure-inducing input that prompted you to make that change


Show the symptom of that failure-inducing input by showing the output of running the file at the command line for the version where it was failing (this should also be in the commit message history)


Write 2-3 sentences describing the relationship between the bug, the symptom, and the failure-inducing input.

## Review
