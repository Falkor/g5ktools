# g5ktools

A set of scripts/configs I use on Grid5000. 
In particular: 

* `g5k-sync-home`: a synchonization script based on `rsync` that permit to easily
  backup/restore part or all your homedir data between the different sites of
  [Grid5000](http//www.grid5000.fr). 

 Note that this assumes you are able to connect by SSH between each site. You can easily achieve that by generating an SSH keypair:

 		(yoursite)$> ssh-keygen -t dsa
		(yoursite)$> cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys

 Now you have to synchronize the `~/.ssh/` directory between the sites, typically by issuing:

		(yoursite)$> g5k-sync-home all .ssh

Now comes the detailed description of the proposed tools.

# Installation

* Setup the directories to host these files: 

		$> cd $HOME
		$> mkdir -p bin git/github.com/Falkor 
		
* Clone the repository - you perhaps also want to clone my `dotfiles` repository:

		$> cd git/github.com/Falkor
		$> git clone https://github.com/Falkor/g5ktools.git
		$> git clone https://github.com/Falkor/dotfiles.git

* Create the appropriate links:

		$> cd ~/bin
		$> ln -s ../git/github.com/Falkor/g5ktools/scripts/g5k-sync-home .

* Setup the `dotfiles`: see [Installation notes on Github](https://github.com/Falkor/dotfiles)

# Description of the `g5ktools` scripts

## == `g5k-sync-home` ==


		NAME
		    g5k-sync-home -- Synchronize the homedir (or any item relative to your homedir)
		    between the different sites of Grid5000
		
		SYNOPSIS
		    g5k-sync-home [-V | -h]
		    g5k-sync-home <site|all> [--debug] [-v] [-n] [--delete] [--retrieve|--push] [item1...]
		
		DESCRIPTION
		    g5k-sync-home synchronize your files and directory (inside your homedir) between
		    the G5K sites using rsync. Example: 
		
		         # upload /Users/svarrette/data from Luxembourg to nancy (simulate)
		         (luxembourg)$> g5k-sync-home nancy --dry-run data
		
		         # synchonize your full homedir with all other sites:
		         (luxembourg)$> g5k-sync-home all --dry-run
		
		         # retrieve the /Users/svarrette/toto from rennes
		         (luxembourg)$> g5k-sync-home rennes --retrieve toto
		
		OPTIONS
		    --delete      Causes g5k-sync-home to delete files on the target if absent in the
		                  original directory. This ensure an exact replica but you may
		                  loose files so use this option with caution.
		    --debug       Debug mode. Causes g5k-sync-home to print debugging messages.
		    -h --help     Display a help screen and quit.
		    -n --dry-run  Simulation mode.
		    -p ---push    Push mode (default). rsync local homedir on the remote site.
		    -r --retrieve Retrieve mode. rsync from the remote site into your local homedir.
		    -v --verbose  Verbose mode.
		    -V --version  Display the version number then quit.
		
		AUTHOR
		    Sebastien Varrette <Sebastien.Varrette@uni.lu>
		    Web page: http://varrette.gforge.uni.lu
		
		REPORTING BUGS
		    Please report bugs using the tracker system available
		    [here](https://github.com/Falkor/g5ktools/issues). Feel free also to contact
		    [me](mailto:Sebastien.Varrette@uni.lu) for comments. 
		
		COPYRIGHT
		    This is free software; see the source for copying conditions.  There is
		    NO warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR
		    PURPOSE.

		RESOURCES
		    The latest version of this script is available on [Github](https://github.com/Falkor/g5ktools)	

# Licence

The proposed scripts are available under the GPL licence -- see the `DISCLAIMER` file. 

# General Grid5000 tips

You can find below interesting links providing information for a better usage of Grid5000:

* [G5K Tips by ASCOLA](http://www.emn.fr/z-info/ascola/doku.php?id=internet:members:fquesnel:g5k_tips)
* [Working efficiently on Grid’5000](https://www.grid5000.fr/school2010/slides/g5kss10-grid5000-efficiently.pdf), a very nice talk by Lucas
* [Towards better experiments on Grid’5000](http://www.loria.fr/~lnussbau/files/renpar11-grid5000.pdf), yet another nice talk by Lucas ;)
* [Large scale tips](https://www.grid5000.fr/mediawiki/index.php/Large_scale_tips)



