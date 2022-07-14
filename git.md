# Using GIT Like a pro

1. Setup your git repository

2. Create an SSH key

In Windows Powershell, this creates a key :

  PS > ssh-keygen
  
3. Add the key to github

  github.com/settings/ssh/new
  Title: MySSHKey
  Key:
  ssh-rsa
  AAAA... localuser@DESKTOP\

4. Clone the repo

  PS > git clone git@github.com:github.com/ololooloolooolll/Active_Directory.git
  PS > mkdir anewdir

5. Setup localhost

  PS > git config --global user.email "username@mydomain.com"
  PS > git config --global user.nam "First Last"
  
6. Push the new directory

  PS > git commit
  Initial commit -- Look at that
  PS > git push
  
