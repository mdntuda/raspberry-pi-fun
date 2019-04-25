Since git 2.13 it is possible to easily handle multiple accounts. 
You need to use backports to upgrade your git because in Debian 9.x Stretch there is version 2.11 of git installed!

`
echo echo "deb http://ftp.debian.org/debian stretch-backports main" || sudo tee /etc/apt/sources.list.d/stretch-backports.list 
sudo apt-get update
sudo apt-get install -t stretch-backports git
`

After that the most stable version of git will be installed.

For saving your credentials you need to use libsecret because gnome-keyring is deprecated. Follow this step from the source: https://askubuntu.com/questions/773455/what-is-the-correct-way-to-use-git-with-gnome-keyring-and-https-repos 

`
sudo apt-get install libsecret-1-0 libsecret-1-dev
cd /usr/share/doc/git/contrib/credential/libsecret
sudo make
git config --global credential.helper /usr/share/doc/git/contrib/credential/libsecret/git-credential-libsecret
`

In `~/.gitconfig` add:
	
	[includeIf "gitdir:~/git-repos/github/"]
        path = ~/git-repos/github/.gitconfig
	
	
	and of course you need to write the `.gitconfig` in the folder `~/git-repos/github/.gitconfig` with your specific credentials
	My `~/git-repos/github/.gitconfig` contains following content: 
		
		[user]
		        email = my-email@gmx.net
        		name = XXXXX YYYYYY
        		username = sigma-ai
		
		
For credentials I add following line to my `~/.gitconfig`
		
	[credential]
	        helper = /usr/share/doc/git/contrib/credential/libsecret/git-credential-libsecret

