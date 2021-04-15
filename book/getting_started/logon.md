# Logging on

```{warning} **Read carefully**
This is a big article that covers lots of important details about logging in especially for those connecting from off campus.
```

Once you have an account you'll be able to connect to the University HPC systems using a secure shell (SSH). In the page below we'll cover how to make sure you can SSH from your machine (installing any prerequired software) and how to configure your SSH to connect from off-campus.

## **Connecting from Linux/MacOS systems**

### SSH via Terminal

Linux and MacOS systems all come with a Terminal application that opens a command-line shell. In the following example code snippets we'll be connecting with the username `exuser`. When you come to log in to a system you'll need to use your own university username in place of `exuser`.

To log in from your Terminal use the following command:

```bash
# to log into ARC4
$ ssh exuser@arc4.leeds.ac.uk

# to log into ARC3
$ ssh exuser@arc3.leeds.ac.uk
```

You will then be prompted for your password which you should enter.

```{note} For security placeholder characters
will not appear as you type your password. Your keystrokes are recorded so please type carefully!
```

### Graphics forwarding (X11)

Secure shell allows X display (GUI) traffic to be tunnelled (and encrypted) through the SSH connection. Provided your local display is set up correctly, the -Y flag can be used to allow trusted X11 forwarding:

```bash
$ ssh -Y exuser@arc4.leeds.ac.uk
```

```{note} **For macOS Users**
The latest versions of macOS do not have an X11 client installed so this will need to be downloaded and installed seperately. X11 for Mac can be obtained from the [XQuartz](http://www.xquartz.org/index.html). This is a dmg file so will prompt you with the correct instructions for installation.
```

### Configuring SSH for off-campus connections

In order to connect to ARC when you're off campus you'll need to do some extra configuration so that your SSH connection goes via our `remote-access` server. The following steps outline how to setup this configuration:

1. Open a Terminal on your Linux/macOS machine
2. Create a directory called `.ssh` in your home directory (if one doesn't already exist)

    ```bash
    $ mkdir ~/.ssh
    ```

3. Then open a text editor of your choice and create a file called `config` in your `.ssh` directory

    ```bash
    # for instance use the simple nano text editor
    $ nano ~/.ssh/config
    ```

4. Within this file include the following contents where `USERNAME` is replaced by your university username

    ```
    Host *.leeds.ac.uk !remote-access.leeds.ac.uk
    ProxyJump USERNAME@remote-access.leeds.ac.uk
    User USERNAME
    ```

    ````{admonition} Old version of SSH
    If you're using an old version of OpenSSH, you may get an error: `Bad configuration option: ProxyJump`.  In this case you'll want to use this instead:

    ```
    Host *.leeds.ac.uk !remote-access.leeds.ac.uk
    ProxyCommand ssh -W %h:%p USERNAME@remote-access.leeds.ac.uk
    User USERNAME
    ```
    ````

5. Save this file and your configuration is all set up!

You will now be prompted for your password twice everytime you attempt to log into ARC, this is because you are logging into the remote-access server first and then connecting to ARC.

## **Connecting from Windows**

Windows by default does not come with an SSH client. Therefore, we need to install an SSH client and an X server for forwarding graphical applications. We recommend using [MobaXTerm](http://mobaxterm.mobatek.net/) which combines an SSH program (similar to PuTTY), a simple file transfer utility, a text editor and an X-Server into a single package.

### Setting up MobaXTerm

To get started you need to install MobaXTerm. You can do this by downloading the **Portable Home edition** [(Click here to go to the download page)](https://mobaxterm.mobatek.net/download-home-edition.html) which is a .zip file containing the software. You can follow the steps in the below video to help walkthrough getting set up.

<iframe src="https://mymedia.leeds.ac.uk/Mediasite/Play/7c25b8af4c7f43f7898efeba0ec6dd311d" width="100%" height="300" frameborder="0" marginwidth="0" marginheight="0" scrolling="auto" allowfullscreen="allowfullscreen" style="display:block;"> </iframe>

### Connecting via MobaXTerm

Once you have MobaXTerm downloaded you can connect to ARC via two mechanisms: using the builtin local terminal to connect using SSH commands; or creating an SSH session via the GUI.

#### Creating an SSH session

You can create an SSH session to connect to ARC using the following steps:

| 1. Open the initial MobaXTerm Menu and select Session |
| ----------------------------------------------------- |
| ![Open the initial MobaXTerm Menu and select Session](../assets/img/logon/mobaXTerm1.png) |

| 2. In the Session Wizard Window select SSH |
| ----------------------------------------------------- |
| ![In the Session Wizard Window select SSH](../assets/img/logon/mobaXTerm2.png) |

| 3. Input the basic setting details for SSH session: the host (address of ARC), the username (your university username) |
| ----------------------------------------------------- |
| ![Input the basic setting details for SSH session: the host (address of ARC), the username (your university username)](../assets/img/logon/mobaXTerm3.png) |

| 4. Select the Network Settings tab within the Session Settings window |
| ----------------------------------------------------- |
| ![Select the Network Settings tab within the Session Settings window](../assets/img/logon/mobaXTerm4.png) |

| 5. Click on the large button labelled "SSH gateway (jump host)" and input details for connecting to remote-access.leeds.ac.uk (Gateway SSH server) and specify your username |
| ----------------------------------------------------- |
| ![Select the "Connect through SSH gateway (jump host) option](../assets/img/logon/mobaXTerm5.png) |

| 6. You will immediately be prompted for your password to connect to the remote-access server |
| ----------------------------------------------------- |
| ![You will immediately be prompted for your password to connect to the remote-access server](../assets/img/logon/mobaXTerm6.png) |

| 7. After it accepts your password it will request your password again, this time to log into ARC4 |
| ----------------------------------------------------- |
| ![After it accepts your password it will request your password again, this time to log into ARC4](../assets/img/logon/mobaXTerm7.png) |

```{note} For security placeholder characters
will not appear as you type your password. Your keystrokes are recorded so please type carefully!
```

| 8. Once successful you will see the ARC4 message of the day and the ARC prompt |
| ----------------------------------------------------- |
| ![Once successful you will see the ARC4 message of the day and the ARC prompt](../assets/img/logon/mobaXTerm8.png) |

| 9. You can restart an existing session after it has closed by double-clicking the session under the User sessions folder on the left-hand panel of the main MobaXTerm menu |
| ----------------------------------------------------- |
| ![You can restart an existing session after it has closed by double-clicking the session under the User sessions](../assets/img/logon/mobaXTerm9.png) |

#### Using the MobaXTerm Terminal

Alternatively, you can connect to ARC using the builtin Terminal within MobaXTerm and use the `ssh` command. 

##### Configuring MobaXTerm Terminal

In order to successfully connect off-campus you are required to adjust some settings within MobaXTerm to create a persistent home directory and create a configuration file for SSH.

| 1. Open the initial MobaXTerm Menu and select Settings |
| ----------------------------------------------------- |
| ![Open the initial MobaXTerm Menu and select Settings](../assets/img/logon/mobaSSH1.png) |

| 2. Select the folder icon on the right-hand side of the Persistent home directory setting box |
| ----------------------------------------------------- |
| ![Select the folder icon on the right-hand side of the Persistent home directory setting box](../assets/img/logon/mobaSSH2.png) |

| 3. Select a folder location to use for your persistent home directory (this can be any writeable folder on your computer), here I am using my C:\User\university_username folder |
| ----------------------------------------------------- |
| ![Select a folder location to use for your persistent home directory](../assets/img/logon/mobaSSH3.png) |

| 4. This takes you back to the MobaXTerm Setting Menu, where you can now select OK  |
| ----------------------------------------------------- |
| ![This takes you back to the MobaXTerm Setting Menu, where you can now select OK](../assets/img/logon/mobaSSH4.png) |

| 5. You will then be prompted to restart MobaXTerm so that the new settings are applied |
| ----------------------------------------------------- |
| ![You will then be prompted to restart MobaXTerm so that the new settings are applied](../assets/img/logon/mobaSSH5.png) |

| 6. When MobaXTerm restarts, select the Start Local Terminal option |
| ----------------------------------------------------- |
| ![When MobaXTerm restarts, select the Start Local Terminal option](../assets/img/logon/mobaSSH6.png) |

| 7. This takes you to the MobaXTerm terminal view |
| ----------------------------------------------------- |
| ![This takes you to the MobaXTerm terminal view](../assets/img/logon/mobaSSH7.png) |

| 8. Next create a folder called `.ssh` using the command `mkdir .ssh` |
| ----------------------------------------------------- |
| ![This takes you to the MobaXTerm terminal view](../assets/img/logon/mobaSSH8.png) |

```{note} If this folder already exists you will get an error saying this file/folder already exists just skip to step 9
```

| 9. Then go to Tools > MobaTextEditor   |
| ----------------------------------------------------- |
| ![This takes you to the MobaXTerm terminal view](../assets/img/logon/mobaSSH9.png) |

| 10. Type the contents of the file as follows where `USERNAME` is your university username |
| ----------------------------------------------------- |
| <pre id="codecell0"> Host *.leeds.ac.uk !remote-access.leeds.ac.uk <br> ProxyJump USERNAME@remote-access.leeds.ac.uk <br> User USERNAME </pre> |
| ![This takes you to the MobaXTerm terminal view](../assets/img/logon/mobaSSH10.png) |

| 11. Once complete go to File > Save As  |
| ----------------------------------------------------- |
| ![Once complete go to File > Save As](../assets/img/logon/mobaSSH11.png) |

| 12. Select the `.ssh` folder you created in the step 8.  |
| ----------------------------------------------------- |
| ![ Select the .ssh folder you created in the step 8.](../assets/img/logon/mobaSSH12.png) |

| 13. Name the file as `config` and press Save and close MobaTextEditor |
| ----------------------------------------------------- |
| ![Name the file as `config` and press Save](../assets/img/logon/mobaSSH13.png) |

And now MobaXTerm should be configured so we can SSH to ARC using the MobaXTerm Terminal.

##### SSHing via the MobaXTerm Terminal

We can use the MobaXTerm Terminal like a standard unix shell to navigate around our local computer and also to SSH onto remote hosts including ARC. In order to connect to ARC we need to make sure we have configured MobaXTerm as described in [the above section](#configuring-mobaxterm-terminal)

| 1. Within a local Terminal on MobaXTerm we use the `ssh` command to connect to ARC |
| ----------------------------------------------------- |
| ![Within a local Terminal on MobaXTerm we use the `ssh` command to connect to ARC](../assets/img/logon/mobaSSH_1.png) |

| 2. We are then prompted to submit our password to connect to `remote-access.leeds.ac.uk` |
| ----------------------------------------------------- |
| ![We are then prompted to submit our password to connect to remote-access](../assets/img/logon/mobaSSH_2.png) |

| 3. We are then prompted to submit our password to connect to `arc4.leeds.ac.uk` |
| ----------------------------------------------------- |
| ![We are then prompted to submit our password to connect to arc4](../assets/img/logon/mobaSSH_3.png) |

| 4. Once we have successfully submitted our passwords our prompt will change and the message of the day for ARC4 will be displayed |
| ----------------------------------------------------- |
| ![ARC4 message of the day on MobaXTerm](../assets/img/logon/mobaSSH_4.png) |
