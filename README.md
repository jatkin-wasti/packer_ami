# Packer
## Installing packer
- Follow the steps in the following [link](https://learn.hashicorp.com/tutorials/packer/getting-started-install/) for your OS
- For Linux this will be:

```curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -```

```sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"```

```sudo apt-get update && sudo apt-get install packer```

- You can then verify the installation was successful by typing `packer` in the terminal and then enter
- This should provide you with a list of available commands for packer
## What are packer files?
- Packer files are written in JSON format
- These files act as a template to build virtual machines by specifying the OS and the state of the hardrive
- It can do this by creatin AMI's in the state that is required
- EC2 Instances can then be created based on that AMI with all of the provisioning already completed
- Services may still need scripts to run or restart them when the instances are created
## Packer file Syntax
