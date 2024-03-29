[Return to Index Page](https://andrewonozuka.github.io/cse15l-lab-reports/index)

# Lab Report 1 | Week 2 | Remote Access Tutorial

## Installing VScode

1 |  Let's first begin by installing VScode! VScode is short for Visual Studio Code, and it a source-code editor made my Microsoft.

2 | [Use this link to download VScode!](https://code.visualstudio.com/download) Make sure you download the right version for your operating system. (macOS, Windows, Linux)

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-04-08%20at%2009.22.27.png?raw=true)

3 | After you have installed VScode, you're ready to go!

## Remotely Connecting

1 | You will encounter course-specific accounts in many of the CSE courses at UCSD. You may also see similar individualized accounts at other institutions or future jobs, so getting used to these will help you in the future!

2 | Open a new terminal in VScode by going to the top of your screen and selecting "Terminal" -> "New Terminal".

3 | Then type:

```
ssh cs15lsp22xxx@ieng6.ucsd.edu
```

*make sure you replace the xxx with your unique three letter sequence! also make sure the quarter info is updated, it says sp22 as it is spring 2022 when this lab report is being written*

4 | The first time you log in, it will ask if you want to continue connecting. Type: "yes", and then press enter.

5 | You will then be prompted for a password. Login using your password that you use for TritonLink!

The whole process should look like this:

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-04-08%20at%2009.46.08.png?raw=true)

## Trying Some Commands

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

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-04-08%20at%2010.11.03.png?raw=true)

## Moving Files with scp

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

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/lORFbWcDjh7nzoRVQXzyWzspJ0KI1RICFO6b55nKb7HCIqC-3_zEGt_9mmPj2OaHdKoZcjn0P_Jv3bjAboM9fVAmkBLMIt3ZtUreiy591fH_mJwq3qGdAJEsYBd7.png?raw=true)

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

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/ZhAV1puUSET361DhEdnOSFe2vjwYE5Elj56vy96iMwLvTcMsIkWuFSS5e1bT7yzrP2ZhP8xVvN7zNZg8vvtTYrh4ucMeQExmmGY_-duAFvBq1pOTNSQr4DG7mN1Q.png?raw=true)

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

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/Screenshots/Screen%20Shot%202022-04-10%20at%2019.09.19.png?raw=true)

Happy remote connecting!
