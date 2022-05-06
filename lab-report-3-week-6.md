In this lab report, you will implement all Group Choice Options (1-3) from Lab 5. Complete them for yourself (if you haven’t already), and take the relevant screenshots listed below. Create a post with a few sentences of description about all the options available. 




[Return to Index Page](https://andrewonozuka.github.io/cse15l-lab-reports/index)

[Link to Lab Report 3 Writeup](https://docs.google.com/document/d/1u_IB3nJrXeve0HvcD1BNMa27yw6uMX4Jz7PXU_xIMP4/edit?usp=sharing)

# Lab Report 3 | Week 6

## Background

In this lab report, we implement all of the group choice options from Lab 5. The link can be found below:

[Link to Lab Report 3 Writeup](https://docs.google.com/document/d/1NQ17hecUPFKeoFyrEvK9DBlCS1JkDbMW6Ygrf_CJJJU/edit?usp=sharing)

## Streamlining ssh Configuration

- Show your .ssh/config file, and how you edited it (with VScode, another program, etc)

To edit my .ssh/config file, I opened up the built-in terminal (as I am on Mac). 

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/screenshots-lr3/Screen%20Shot%202022-05-06%20at%2011.40.14.png?raw=true)

As you can see, I typed:

```
cd ~/.ssh           # change directory
ls -a               # list all
cat config          # to see the contents of config
vim config          # to edit config
```

After typing the last vim command, your screen should turn into something like this:

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/screenshots-lr3/Screen%20Shot%202022-05-06%20at%2012.13.02.png?raw=true)

To edit the file, press the "i" key (insert) and then make your changes. Once you are done, press the "esc" key (escape) and type ":wq" then press "enter". This will bring you back to the terminal. After these changes, you should be able to directly log on with a shorter ssh command:

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/screenshots-lr3/Screen%20Shot%202022-05-06%20at%2012.18.45.png?raw=true)

If we edit the first line of the config file after "Host", we can actually use whatever phrase we want. Below is an example:

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/screenshots-lr3/Screen%20Shot%202022-05-06%20at%2012.21.44.png?raw=true)

```
ssh lr3ex           # lab report 3 example
```

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/screenshots-lr3/Screen%20Shot%202022-05-06%20at%2012.21.30.png?raw=true)

- Show an scp command copying a file to your account using just the alias you chose.

## Setup Github Access from ieng6

- Show where the public key you made is stored on Github and in your user account (screenshot).
- Show where the private key you made is stored on your user account (but not its contents) as a screenshot.
- Show running git commands to commit and push a change to Github while logged into your ieng6 account.
- Show a link for the resulting commit.

Screenshot of code change diff from Github:

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-05-01%20at%2005.12.43.png?raw=true)

[Failure Inducing Input: test-file4.md](https://github.com/andrewonozuka/markdown-parser/edit/main/test-file4.md)

Another bug we encountered was how to deal with links in the form of screenshots. Because images are in the format ! + [image name] + (image address), the program would encounter an error and end up stuck in an infinite loop.

Failing Output #2:

![Failing Output #2](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-05-01%20at%2005.36.55.png?raw=true)

After our code change, we can now successfully process input files with image links also. Since we are looking to return URL links only, the lines with links in an image format are simply ignored and only the remaining valid links are returned.

Passing Output #2:

![Passing Output #2](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-05-01%20at%2005.37.06.png?raw=true)

## Copy whole directories with scp -r

- Show copying your whole markdown-parse directory to your ieng6 account.
- Show logging into your ieng6 account after doing this and compiling and running the tests for your repository.
- Show (like in the last step of the first lab) combining scp, ;, and ssh to copy the whole directory and run the tests in one line.

Screenshot of code change diff from Github:

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-05-01%20at%2005.14.59.png?raw=true)

[Failure Inducing Input: test-file3.md](https://github.com/andrewonozuka/markdown-parser/edit/main/test-file3.md)

While we addressed the issue of the infinite loop earlier, our solution only had an if and else if statement. Because it was missing the last else statement, it was not properly returning the expected output.

Failing Output #3:

![Failing Output #3](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-05-01%20at%2005.07.20.png?raw=true)

The bug was with input lines that were missing parenthesis. Once we added the last else statement so that all cases were covered, we were able to successfully ignore the faulty lines of input and only return the valid links.

Passing Output #3:

![Passing Output #3](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-05-01%20at%2005.07.30.png?raw=true)

## Final Review

After all of our code changes, this is what our code now looks like:

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

            if (openBracket == -1 || closeBracket == -1 || openParen == -1 || closeParen == -1) {
                currentIndex = markdown.length();
                break; // prevents infinite loop
            } else if (closeBracket + 1 == openParen && openBracket != -1) {
                if (markdown.indexOf("\n", openBracket) < closeParen) {
                    currentIndex = closeParen;
                } else if (markdown.charAt(openBracket - 1) == '!') {
                    currentIndex = closeParen + 1; 
                } else {
                    toReturn.add(markdown.substring(openParen + 1, closeParen));
                    currentIndex = closeParen + 1;
                }
            } else {
                toReturn.add(markdown.substring(openParen + 1, closeParen));
                currentIndex = closeParen + 1;
            }
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

Code Change Diff (Final):

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-05-01%20at%2005.44.45.png?raw=true)