[Return to Index Page](https://andrewonozuka.github.io/cse15l-lab-reports/index)

[Link to Lab Report 3 Writeup](https://docs.google.com/document/d/1u_IB3nJrXeve0HvcD1BNMa27yw6uMX4Jz7PXU_xIMP4/edit?usp=sharing)

# Lab Report 3 | Week 6

## Background

In this lab report, we implement all of the group choice options from Lab 5. The link can be found below:

[Link to Lab Report 3 Writeup](https://docs.google.com/document/d/1NQ17hecUPFKeoFyrEvK9DBlCS1JkDbMW6Ygrf_CJJJU/edit?usp=sharing)

## Streamlining ssh Configuration

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

This updates shortened alias is helpful with other commands as well. Here is an example of using an scp command to move a file:

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/screenshots-lr3/Screen%20Shot%202022-05-06%20at%2012.32.57.png?raw=true)

## Setup Github Access from ieng6

Your public key should be stored as a "id_rsa.pub" file as seen below:

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/screenshots-lr3/Screen%20Shot%202022-05-06%20at%2012.45.36.png?raw=true)

Your private key should be stored as a "id_rsa" file as seen below:

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/screenshots-lr3/Screen%20Shot%202022-05-06%20at%2012.38.08.png?raw=true)

You can also use git commands to add, commit, and push changes to Github through the terminal using these commands:

```
git add lab-report-3-week-6.md
git commit lab-report-3-week-6.md
git push
```

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/screenshots-lr3/Screen%20Shot%202022-05-06%20at%2013.11.09.png?raw=true)

Here's what it looks like on Github:

[Resulting Commit](https://github.com/andrewonozuka/cse15l-lab-reports/commit/cd253a79af4ffcb265e59b3922009ad126df2f4d)

![Screenshot](https://github.com/andrewonozuka/cse15l-lab-reports/blob/main/screenshots-lr3/Screen%20Shot%202022-05-06%20at%2013.12.58.png?raw=true)

## Copy whole directories with scp -r

Here's what it looks like when you copy your whole markdown-parse directory into your ieng6 acount:

![Screenshot]()

- Show logging into your ieng6 account after doing this and compiling and running the tests for your repository.
- Show (like in the last step of the first lab) combining scp, ;, and ssh to copy the whole directory and run the tests in one line.
