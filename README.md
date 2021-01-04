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
- Packer files are written in JSON format, so to create a packer file simple run `touch filename.json`
- These files act as a template to build virtual machines by specifying the OS and the state of the hardrive
- It can do this by creatin AMI's in the state that is required
- EC2 Instances can then be created based on that AMI with all of the provisioning already completed
- Services may still need scripts to run or restart them when the instances are created
## Packer file Syntax
- Whitespace isn't important for json format, but make sure you adhere to the key value format of the JSON file
- This means that we'll need `"key": "value"` pairs
- If an item is opened with `{` or `[` we need to make sure we close it correctly
- Variables can be used `{{ \`like_this\`}}`
- Before the variable you specify where the variable can be found
- `user` can be placed before like_this in our example to be used from a variable section defined at the beginning of the packer file
- This section is placed above the builders section and stores the variables you wish to use
## Packer commands
- `packer validate filename.json` checks the validity of the packer file, giving you information on what syntax errors exist and where
- `packer build filename.json` will run the packer file and attempt to create the AMI
## Getting our packer file working
- We wrote to our packer file using [this](https://learn.hashicorp.com/tutorials/packer/getting-started-build-image?in=packer/getting-started) template as a base
- We will change:
  - the region to the region that we use (eu-west-1)
  - the name in the ami filter to find the OS that we want
  - the ami_name to a name that follows your companies naming convention
- We want to keep our aws keys secure so we'll export them in our bashrc file as environment variables and then referencing them in our variables section
- To provision the AMI, we add a provisioners section and specify how we're going to achieve this
- We'll use an ansible file so we'll specify the type as ansible and then the playbook file that it should run
- We'll also run a shell command to start the app
- Now that our packer file is built we'll run it and see it successfully create an AMI! (Don't worry if this takes a while)
- Once this is complete, we can create an EC2 instance using the recently made AMI and it should have all the relevant services and packages installed, with the app directory copied over
- All that needs to be done to get the app working is to ssh into this new instance, cd into the app directory, and run `pm2 start app.js`
- Congratulations! We've created a template to get new instances set up with our app working with minimal effort!
