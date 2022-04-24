
[Return to Index Page](https://andrewonozuka.github.io/cse15l-lab-reports/index)

[Link to Lab Report 2 Writeup](https://docs.google.com/document/d/14SJ2qRuxBCfOXxI1-dPo3KTOvd4bmM0K25GyVtfXLrU/edit)

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

Failing Output #1:

![Failing Output #1](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screen%20Shot%202022-04-24%20at%2005.44.48.png?raw=true)

Passing Output #1:

![Passing Output #1](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screen%20Shot%202022-04-24%20at%2005.45.34.png?raw=true)

Without the break statement, the while loop runs forever. This means the program never stops and we never get an output. By checking if any of the parameters are -1, we know to break the loop and output the correct list of links.

## Code Change #2

Screenshot of code change diff from Github:

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screen%20Shot%202022-04-24%20at%2005.59.36.png?raw=true)

[Failure Inducing Input #2](https://github.com/andrewonozuka/markdown-parser/edit/main/test-file2.md)

Failing Output #2:

![Failing Output #2](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screen%20Shot%202022-04-24%20at%2006.02.39.png?raw=true)

Passing Output #2:

![Passing Output #2](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screen%20Shot%202022-04-24%20at%2006.02.27.png?raw=true)

When attempting to fix the bugs, I moved the original

```
toReturn.add(markdown.substring(openParen + 1, closeParen));
currentIndex = closeParen + 1;
```

into an if / else if / else statement, but did not have the two lines of code outside. This was causing another infinite loop. Once I added it back in, it was able to work.

## Code Change #3

Screenshot of code change diff from Github:

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screen%20Shot%202022-04-24%20at%2005.51.49.png?raw=true)

[Failure Inducing Input #3](https://github.com/andrewonozuka/markdown-parser/edit/main/test-file3.md)

Failing Output #3:

![Failing Output #3]()

Passing Output #3:

![Passing Output #3]()

Write 2-3 sentences describing the relationship between the bug, the symptom, and the failure-inducing input.

We are able to ignore faulty lines of input that are missing parenthesis. 