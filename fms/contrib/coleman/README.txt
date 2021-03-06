==================================================================================

EDIT JC Bagneris 2012/02/27

To avoid messing with fms itself, I created (in v0.1.9) the contrib directory structure
where any contributed classes can be stored. The path should be 
'contrib/<yourname>/{agents,worlds,engines,markets}/'.

Thus you'll find here the contributions of P. Coleman and S. Nazif.
I edited the agentfile.txt to make it work in the new framework and dropped
non-classes contributions of Coleman & Nazif in 'contrib/coleman/'.

Everything should work with unmodified fms now.

==================================================================================

Dependencies:
	PyYAML
	Financial Market Simulator (fms) by JC Bagneris

Installing Dependencies:
	
	PyYAML - Simply download the package from pyyaml.org or use aptitude or a similar utility to install.

	fms - We have provided a modified package of the fms utility with our submission. To install the package simply run from the root jcbagneris-fms directory the command: "sudo python setup.py install".

Code Organization:

	The files we personally wrote are somewhat mixed into the pre-existing files provided by fms. In general, the home directory (containing startfms.py and cleanstart.sh) is the hub for the execution files.  Upon running the cleanstart.sh, output files from previous experiments are cleaned up and the tournament is restarted using the agents in "agentfile.txt". In this way, new implementations of the agent interface (stored in /fms/agents) can be added to the pool by simply adding the classname to "agentfile.txt".  The checksuccess.py file holds the bulk of the tournament code, which essentially generates the experiment (.yml) files needed to simulate the different agent head to head markets and then instructs the fms to run on each experiment file, generating "ultimateoutput.txt" that is parsed from the output files of each individual step (exp0wealth.csv etc.).

Important files (that we have implemented or modified significantly):

All agent behavior classes in /fms/agents except ZeroIntelligence and RandomTrader(this class also uses a different set of parameters and should not be added to "agentfile.txt")

asynchronousramdwreplace.py in /fms/engines - modified to output wealth states, initially the only output was the transaction log of each simulation

checksuccess.py - Does the work to set up and parse the output of the 
"tournament of agents"

cleanstart.sh - cleans up leftover output and starts anew

agentfile.txt - List of classes which are stored in /fms/agents that are intended for inclusion in the next simulation run.

Running the simulation:

Simulations are run by parsing a .yml configuration file which is generated by checksuccess.py, but should always be run by calling "sh cleanstart.sh" to avoid retaining old outputs.

Currently all agents are enabled by default in "agentfile.txt". A previous run of the output of a run of all agents and then the top half of that run is saved in files "allagentsrunout.txt" and "tophalfrunout.txt" respectively (for convenience, since simulation takes a while).

	
