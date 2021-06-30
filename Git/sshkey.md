First check if there are any keys
To check if there are any existing SSH keys on your PC:

  ls -al ~/.ssh
  
To create a new SSH key, run the following command substituting in your GitHub email address without ""

  ssh-keygen -t rsa -b 4096 -C "YOUR_GITHUB_EMAIL_ADDRESS"


add key to github -> Navigate to SSH and GPG keys section.

  cat ~/.ssh/id_rsa.pub
  
Run the following command, to test your entire SSH key setup.

  ssh -T git@github.com
  
Adding your SSH key to the ssh-agent
  
   eval \$(ssh-agent -s)
   
   // delete all key 
   ssh-add -D
   
   // add the generated key to the agent
   ssh-add ~/.ssh/id_rsa
   
   // check: list the added keys:
   ssh-add -l


CHange repo : to ssh instead of account

  remote set-url origin git@github.com:USER/REPO.git
