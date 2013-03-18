# Setting up git and modman for a new module
## Create a new git bare repository

Let's assume we want to create a new module "Magentotutorial_Weblog"

Open a console, create a new folder in the git master directory

<!-- language: lang-bash -->
	
	cd /home/dev/Dropbox/git-master-magento
	mkdir Magento-Module-Magentotutorial_Weblog.git

Navigate into the new folder and create a git bare repository.

<!-- language: lang-bash -->

	cd "Magento-Module-Magentotutorial_Weblog.git"
    git init --bare

![Screenshot of new bare repository](files/new-git-bare-repo.png)

## Create a temporary local repository clone

Open a console and create a temporary directory a local git repository.

<!-- language: lang-bash -->

	 cd /home/dev/workspace
	 mkdir git-tmp
	 cd git-tmp
	 git init

Add the previously created bare repository as remote repository.

<!-- language: lang-bash -->

	git remote add origin /home/dev/Dropbox/git-master-magento/Magento-Module-Magentotutorial_Weblog.git

Apply a local change

<!-- language: lang-bash -->

	touch newfile.txt
	git add .
	git commit -am "first local change"

Push the change to the origin (bare repository)
	
<!-- language: lang-bash -->

	git push origin master

## Configure netbeans for the new repository


Open the clone wizard
![Screenshot open the git clone wizard](files/netbeans-clone-repo1.png)

Select the path od the bare repository
![Screenshot open the git clone wizard](files/netbeans-clone-repo2.png)

Select the branch (there should only be master for now)
![Screenshot open the git clone wizard](files/netbeans-clone-repo3.png)

Select a path for the netbeans project (can stay as is, but copy the path for later)
![Screenshot open the git clone wizard](files/netbeans-clone-repo4.png)

Now Netbeans asks you wether you want to create a new project. - This is the same wizard as File->New Project.

Select PHP Application from Existing Sources
![Screenshot open the git clone wizard](files/netbeans-create-project1.png)

Paste the path of the newly created netbeans project
![Screenshot open the git clone wizard](files/netbeans-create-project2.png)

Just click continue and leave everything as is.
![Screenshot open the git clone wizard](files/netbeans-create-project3.png)

This is how your Netbeans project tabs should look like:
![Screenshot open the git clone wizard](files/netbeans-create-project4.png)

---

language: en
date: 2013-03-15
tags: Magento, modman, Deployment