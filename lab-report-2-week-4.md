
[Return to Index Page](https://andrewonozuka.github.io/cse15l-lab-reports/index)

[Link to Lab Report 2 Writeup](https://docs.google.com/document/d/14SJ2qRuxBCfOXxI1-dPo3KTOvd4bmM0K25GyVtfXLrU/edit)

# Lab Report 2 | Week 4 | Fixing Markdown Parser

## Background

In the lab for week 3, we took a look at MarkdownParse.java, which initially looks something like this:

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

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-05-01%20at%2005.13.07.png?raw=true)

[Failure Inducing Input: test-file.md](https://github.com/andrewonozuka/markdown-parser/edit/main/test-file.md)

The initial code does not take into account the scenario when a test file is missing brackets. Because the code looks for the characters in a certain order, problems appear when certain characters are not found or are in a different order than expected. Below we can see that the while loop becomes an infinite loop as a result.

Failing Output #1:

![Failing Output #1](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-05-01%20at%2005.24.24.png?raw=true)

Once we added the break statement (we used the built-in -1 feature to check if the next expected character was not found), we were able to successfully return an output instead of running into an infinite loop.

Passing Output #1:

![Passing Output #1](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-05-01%20at%2005.24.31.png?raw=true)

## Code Change #2

Screenshot of code change diff from Github:

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-05-01%20at%2005.12.43.png?raw=true)

[Failure Inducing Input: test-file4.md](https://github.com/andrewonozuka/markdown-parser/edit/main/test-file4.md)

Another bug we encountered was how to deal with links in the form of screenshots. Because images are in the format ! + [image name] + (image address), the program would encounter an error and end up stuck in an infinite loop.

Failing Output #2:

![Failing Output #2]()

Passing Output #2:

![Passing Output #2]()

## Code Change #3

Screenshot of code change diff from Github:

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-05-01%20at%2005.14.59.png?raw=true)

[Failure Inducing Input: test-file3.md](https://github.com/andrewonozuka/markdown-parser/edit/main/test-file3.md)

While we addressed the issue of the infinite loop earlier, our solution only had an if and else if statement. Because it was missing the last else statement, it was not properly returning the expected output.

Failing Output #3:

![Failing Output #3](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-05-01%20at%2005.07.20.png?raw=true)

The bug was with input lines that were missing parenthesis. Once we added the last else statement so that all cases were covered, we were able to successfully ignore the faulty lines of input and only return the valid links.

Passing Output #3:

![Passing Output #3](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-05-01%20at%2005.07.30.png?raw=true)