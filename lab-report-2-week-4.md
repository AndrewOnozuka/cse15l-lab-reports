
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


Show a screenshot of the code change diff from Github (a page like this)

Link to the test file for a failure-inducing input that prompted you to make that change


Show the symptom of that failure-inducing input by showing the output of running the file at the command line for the version where it was failing (this should also be in the commit message history)


Write 2-3 sentences describing the relationship between the bug, the symptom, and the failure-inducing input.


![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screen%20Shot%202022-04-08%20at%2009.46.08.png?raw=true)

## Code Change #2

1 | Now that you've been able to securely connect to the remote client, let's try running some commands!

2 | Here are some commands to try:

```
pwd # print working directory
cd ~ # change directory
cd .. # go back one directory
cd ../.. # go back two directories
ls -lat # list laterally
ls -a # list all
```

3 | Here's an example of what it might look like:

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screen%20Shot%202022-04-08%20at%2010.11.03.png?raw=true)

## Code Change #3

1 | Now that you've been introduced to some basic commands, let's try to move files!

2 | For this example, I'm using WhereAmI.java, which I have copied below:

```
class WhereAmI {
  public static void main(String[] args) {
    System.out.println(System.getProperty("os.name"));
    System.out.println(System.getProperty("user.name"));
    System.out.println(System.getProperty("user.home"));
    System.out.println(System.getProperty("user.dir"));
  }
}
```

3 | Try compiling and running the code on your client. You should see your OS, username, current directory, etc.

4 | Then type in the command:

```
scp WhereAmI.java cs15lsp22xxx@ieng6.ucsd.edu:~/
```
You will then be prompted to enter your password.

5 | Once that is complete, you will be able to see that the file has moved over, using "ls". You should see that "WhereAmI.java" is now in the remote server.

6 | If you compile and run it on ssh, you will now see a different result.

Below is my example from lab 1:

![Screenshot](https://github.com/andrewonozuka/markdown-parser/blob/main/Screen%20Shot%202022-04-24%20at%2005.22.21.png?raw=true)

## Setting an SSH Key

1 | So far, we have had to re-type our password everytime to access ssh. Since this is inefficient and redundant over time, there is a way to get around this.

2 | In your terminal, type in:

```
ssh-keygen
```

3 | You will then be asked to "Enter file in which to save the key"

```
(/Users/<user-name>/.ssh/id_rsa): /Users/<user-name>/.ssh/id_rsa
```

4 | When asked to "Enter passphrase", make sure to enter NOTHING and simply return twice. You will then see your key's randomart image.

5 | Afterwards, go back to ssh and enter your password. Using "mkdir" (make directory), type:

```
mkdir .ssh
```

6 | Logout, then type:

```
scp /Users/<user-name>/.ssh/id_rsa.pub cs15lsp22zz@ieng6.ucsd.edu:~/.ssh/authorized_keys
```

You have successfully set up an ssh key! It should look similar to this:

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/ZhAV1puUSET361DhEdnOSFe2vjwYE5Elj56vy96iMwLvTcMsIkWuFSS5e1bT7yzrP2ZhP8xVvN7zNZg8vvtTYrh4ucMeQExmmGY_-duAFvBq1pOTNSQr4DG7mN1Q.png?raw=true)

## Optimizing Remote Running

Finally, let's go over some useful things to know to make remote running easier!

- Instead of ssh-ing and then running a command, you can type it directly after the ssh command in the terminal:

```
ssh cs15lsp22xxx@ieng6.ucsd.edu "ls"
```

- You can also use semicolons and call multiple commands:

```
cp WhereAmI.java OtherMain.java; javac OtherMain.java; java WhereAmI
```
- You can also use the up arrow key to scroll back through the commands you have previously typed before, similar to a calculator! This is helpful if you accidentally made a typo at the end or just want to call a command again.

Here's my example:

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screen%20Shot%202022-04-10%20at%2019.09.19.png?raw=true)

Happy remote connecting!
