# SSH Without Password Between Two Linux Computers

Having to constantly type in your password on a Linux server that you SSH to often can be an annoyance. Luckily, this is an easy problem to solve. This guide provides step-by-step instructions to set up SSH key-based authentication, so you no longer need to enter your password.

## Prerequisites

- Two Linux computers (server1 and server2)
- SSH access to both servers

## Steps

### 1. Generate a Public/Private Key Pair on Server1

First, connect to `server1` and generate a public/private key pair.

```bash
ssh-keygen -t rsa
```

When prompted to answer several questions, just hit `Enter` each time until you are returned to a prompt.

```bash
Generating public/private rsa key pair.
Enter file in which to save the key (/home/local/myusername/.ssh/id_rsa): 
Created directory '/home/local/myusername/.ssh'.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/local/myusername/.ssh/id_rsa.
Your public key has been saved in /home/local/myusername/.ssh/id_rsa.pub.
The key fingerprint is:
15:68:47:67:0d:40:e1:7c:9a:1c:25:18:be:ab:f1:3a myusername@server1
The key's randomart image is:
+--[ RSA 2048]----+
|        .*Bo=o   |
|       .+o.*  .  |
|       ...= .    |
|         + =     |
|        S +      |
|         .       |
|      . .        |
|      E+         |
|      oo.        |
+-----------------+
```

Now, copy the public key you just generated. Ensure the text is all on one line to avoid issues later.

```bash
cd .ssh
cat id_rsa.pub
```

Example output (your actual key will differ):

```plaintext
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAyFS7YkakcjdyCDOKpE4RrBecRUWShgmwWnxhbVNHmDtJtK
PqdiLcsVG5PO94hv3A0QqlB1MX33vnP6HzPPS7L4Bq+5plSTyNHiDBIqmZqVVxRbRUKbP44BaA9RsW2ROu
8qdzmXRPupkyFBBOLa23RJJojBieFGygR2OwjS8cq0kpZh1I3c1fbU9I5j38baUK0naTBe2v7s/C8allnJ
hwkfds+Q9/kjaV55pMZIh+9jhoA8acCA6B55DYrgPSycW6fEyV/1PIER+a5lOXp1QCn0U+XFTb85dp5fW0
/rUnu0F9nBJFlo7Rvc1cMuSUiul/wvJ8tzlOhU8FUlHvHqoUUw== myusername@server1
```

### 2. Copy the Public Key to Server2

Next, SSH to `server2` and add the public key to the `authorized_keys` file.

```bash
mkdir -p ~/.ssh
cd ~/.ssh
vi authorized_keys
# paste the public key from server1
chmod 600 authorized_keys
```

### 3. Test the Setup

Finally, test that your setup is working.

```bash
ssh myusername@server2_IP
# you should not be prompted for a password! make sure username and ip collected from server 2
To get IP, run 
ifconfig 
```

If the setup is correct, you will not be prompted for a password when SSHing from `server1` to `server2`.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please fork the repository and submit pull requests for any improvements.

```

In this template:

- **Prerequisites**: Describes the requirements before starting the setup.
- **Steps**: Detailed step-by-step instructions to set up SSH without a password.
- **License**: Information about the project's license.
- **Contributing**: Invitation for contributions.

Replace placeholders like `myusername`, `server1`, and `server2` with your actual usernames and server names. Ensure the public key example is representative of a typical RSA key but remind users that their key will be unique.
