Release Setup
These setup steps only need to be performed on a particular machine once.

Developers using Linux workstations can skip over the references to Cygwin. If using Windows, install cygwin, including Utils/gnupg and Net/openssh packages.

Create and install a SSH key

Open a shell window. If using Windows, open a cygwin window.
Use ssh-keygen to create an SSH key.
Follow the latest steps and guides on the ASF website as you should NOT be using SHA1 and new keys MUST be at least 4096 bits.

   $ ssh-keygen -t rsa -b 4096
Program defaults should be fine. No passphrase is required for the ssh key generation. The keys will be saved in ~/.ssh/id_dsa (private) and ~/.ssh/id_dsa.pub (public).

See Authenticating By Public Key (OpenSSH) for a good description on why and how to perform this task.

SCP your SSH public key ~/.ssh/id_dsa.pub created in last step to ~/id_dsa.pub on people.apache.org.
$ cd ~/.ssh
$ scp id_dsa.pub @people.apache.org:id_dsa.pub
$ You will be prompted for your password.

Use ssh to login to people.apache.org

$ cd ~
$ ssh @people.apache.org

At this point, you will still be prompted for your password.

Create a ~/.ssh folder in your home directory on people.apache.org and change its file mode to 700.

$ mkdir ~/.ssh
$ chmod 700 ~/.ssh
Move or append ~/id_dsa.pub to ~/.ssh/authorized_keys and change its file mode to 600.

$ mv ~/id_dsa.pub ~/.ssh/authorized_keys $ chmod 600 ~/.ssh/authorized_keys

*Each public key in the authorized_keys spans only one line.
For example: "ssh-dss AAAAB3NzaC1kc3MAAA ..... agBmmfZ9uAbSqA== dsa-key-20071107"
'#' in the first column is a comment line.*
Exit out of this ssh session.

Start a new ssh session. No login should be required this time due to the private ssh key on your local box matching up with the public ssh key in your home directory (~/.ssh).

$ ssh @people.apache.org

If you are still prompted for a password, then you have not set up the ssh keys properly. Review the steps above and ensure that all of the steps were followed properly. Or, maybe the instructions are still not quite right and they still need some adjusting. In that case, please update the instructions accordingly.

Create a GPG key

Open a shell window. If using Windows, open a cygwin window.
Generate a key-pair with gpg, using default key kind ("RSA and RSA") and keys size (4096).

$ gpg --gen-key

The program's default values should be fine. For the "Real Name" enter your full name (ie. Stan Programmer). For the "e-mail address" enter your apache address (ie. sprogrammer@apache.org). You will also be required to enter a "passphrase" for the GPG key generation. Keep track of this as you will need this for the Release processing.

The generated keys are stored in $HOME/.gnupg or %HOME%\Application Data\gnupg subdirectory.

Save the content in this subdirectory to a safe media. This contains your private key used to sign all the Streams release materials.

Backup your home directory to another media ||

Add your public key to the SVN repository. See the commands describe at the beginning of this KEYS file to perform this task. The gpg key-pair is used to sign the published artifacts for the Streams releases.

$ gpg --list-sigs && gpg --armor -- export

The KEYS file is updated via normal svn commit procedures. The one under w.a.o/dist/ has to be manually updated from svn.

Submit your public key to a key server. E.g. SURFNET or MIT

Following the instructions in http://people.apache.org/~henkp/trust/ and ask multiple (at least 3) current Apache committers to sign your public key.

Configure Maven

Update your ~/.m2/settings.xml with the properties from Publishing Maven Artifacts
