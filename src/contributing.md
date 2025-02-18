# Contibuting to the ProLUG Linux Sysadmin Course Book

## Signing your Git Commits with SSH
* Generate an SSH key pair if you don't have one:
  ```bash
  ssh-keygen -t ed25519 -C "optional comment"
  ```
* Add SSH public key to github as "Signing Key".  
    * Settings -> GPG and SSH Keys -> Add SSH Key -> Dropdown -> Signing Key
* Configure git locally to use the SSH key to sign your commits.
    * Here's a script that will do that.  
      ```bash
      #!/bin/bash
      GH_USERNAME="YourUsername"
      git config --global user.signingkey "/home/${GH_USERNAME}/.ssh/id_ed25519"
      git config --global gpg.format ssh
      git config --global tag.gpgsign true
      git config --global user.signingkey ~/.ssh/id_ed25519.pub
      git config --global commit.gpgSign true
      mkdir -p ~/.config/git
      touch ~/.config/git/allowed_signers
      echo "${GH_USERNAME} $(cat ~/.ssh/id_ed25519.pub)" > ~/.config/git/allowed_signers
      git config --global gpg.ssh.allowedSignersFile ~/.config/git/allowed_signers
      # Make a commit to verify
      git log --show-signature -1
      ```

## Syncing your Fork with the Original 
You'll need to keep your local fork of the repository up to date with the original repository.  
You can do this from the GitHub web UI easily with the `Sync Fork` button.  
If you want to do this from the terminal, you can add a new `git remote` called `upstream`.  
```bash
git remote add upstream https://github.com/ProfessionalLinuxUsersGroup/lac.git
```
Then, to sync your local fork with the original repo, do a `git pull` from the `upstream` remote.  
```bash
git pull upstream main
```

unit1ws

Treasure 🦆
