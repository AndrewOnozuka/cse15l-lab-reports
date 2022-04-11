[Return to Index Page](https://andrewonozuka.github.io/cse15l-lab-reports/index)

# Lab Report 1 | Week 2 | Remote Access Tutorial

## Installing VScode

1. Let's first begin by installing VScode! VScode is short for Visual Studio Code, and it a source-code editor made my Microsoft.

2. [Use this link to download VScode!](https://code.visualstudio.com/download) Make sure you download the right version for your operating system. (macOS, Windows, Linux)

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screen%20Shot%202022-04-08%20at%2009.22.27.png?raw=true)

3. After you have installed VScode, you're ready to go!

## Remotely Connecting

1. You will encounter course-specific accounts in many of the CSE courses at UCSD. You may also see similar individualized accounts at other institutions or future jobs, so getting used to these will help you in the future!

2. Open a new terminal in VScode by going to the top of your screen and selecting "Terminal" -> "New Terminal".

3. Then type:

"ssh cs15lsp22xxx@ieng6.ucsd.edu"

*make sure you replace the xxx with your unique three letter sequence! also make sure the quarter info is updated, it says sp22 as it is spring 2022 when this lab report is being written*

4. The first time you log in, it will ask if you want to continue connecting. Type: "yes", and then press enter.

5. You will then be prompted for a password. Login using your password that you use for TritonLink!

The whole process should look like this:
![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screen%20Shot%202022-04-08%20at%2009.46.08.png?raw=true)

## Trying Some Commands

1. Now that you've been able to securely connect to the remote client, let's try running some commands!

2. Here are some commands to try:

pwd # print working directory

cd ~ # change directory

cd .. # go back one directory

cd ../.. # go back two directories

ls -lat # list laterally

ls -a # list all

3. Here's an example of what it might look like:
![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screen%20Shot%202022-04-08%20at%2010.11.03.png?raw=true)

## Moving Files with scp

1. Now that you've been introduced to some basic commands, let's try to move files!

2. For this example, I'm using WhereAmI.java, which I have copied below:

class WhereAmI {
  public static void main(String[] args) {
    System.out.println(System.getProperty("os.name"));
    System.out.println(System.getProperty("user.name"));
    System.out.println(System.getProperty("user.home"));
    System.out.println(System.getProperty("user.dir"));
  }
}


## Setting an SSH Key


## Optimizing Remote Running

