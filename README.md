### Title
Using an Interactive Genetic Algorithm and Markov Chain to Compose Melodies Relevant to the User's Taste

### Author
Alireza Samar

### Abstract
Music can be created by anything; it is the melody, which leaves a lasting impression. Simulating the process of evolution on a computer allows one to witness and influence the creation of melodies. I propose a technique to have the computer compose simple, but euphonic melodies by using a Markov chain and an Interactive Genetic Algorithm (IGA). A Markov chain is created from a user selected corpus, and is used to generate the initial population where individuals resemble musical segments the user enjoys. As a result, the initial population will consist of individuals relevant to the user's musical taste. Coupling the Markov chain with an IGA that allows the user to make modifications to each melody by re-ordering the notes, decreases the total number of generations the IGA needs to run for. Additionally, the type of interaction that the fitness function provides is much more engaging and fun for the user than previous approaches, which results in a decreased user burnout rate.

### Requirements
This project has only been tested with:
* Python 2.7
* Chrome (your browser MUST be based on webkit otherwise you will not hear any music!)
* OS X

#### Python Package Manager (pip)
You must have `pip` already installed on your system. If you do not, then the installation script **WILL** fail. I have provided [instructions for installing pip](#installing-pip). You cannot proceed with the installation process until `pip` is available on your system.

#### Installation Script
An installation script, `setup.sh`, has been provided to download the necessary pre-requisites. In order to run
the installation script, you must make it executable otherwise `VirtualEnv` will fail to activate, resulting in
errors when installing libraries from `pip`.
```bash
% chmod +x setup.sh
% ./setup.sh
```

The installation script (`setup.sh`) does the following things:
* Downloads `redis-2.8.2`
* Unzips `redis-2.8.2`
* Compiles Redis
* Copies the Redis conf file from `./bin/redis.conf` to `./bin/redis-2.8.2`
* Deletes the `redis-2.8.2.tar.gz` that was downloaded
* Downloads `VirtualEnv` for Python
  * Creates a sandboxed environment to avoid cluttering your system's Python path
  * This step requires `sudo` because `VirtualEnv` must be installed to your default Python path, heh
* Installs the necessary third party libraries from `pip`, which are found in `requirements.txt`

### Usage
#### Starting the Redis Server
Open up a new shell and set your current working directory to the root level of this project (`./alireza_thesis/code`).

##### Sanity check
```bash
% pwd
/some/directory/structure/alireza_thesis/code
```

Start the Redis server via:
```bash
% ./bin/redis-2.8.2/src/redis-server
```

##### Redis Sanity Check (Making sure you're running the correct Redis database)
To make sure you're running the correct server, open up a new shell and set your current working directory to the root level of this project (`./alireza_thesis/code`). Next, start the Redis client via:
```bash
./bin/redis-2.8.2/src/redis-cli
keys *
```
You should see a bunch of entries (keys) appear. You can leave the `redis-cli` shell by typing `exit` or sending a `CTRL+C` signal. You can come back to the Redis client later to experiment and see the various states of the GA.

#### Starting the Python Server
Open up a new shell and set your current working directory to the root level of this project (`./alireza_thesis/code`).
Next, actiave Virtual Environment via:
```bash
source virtual/bin/activate
```
By running the above command, you are activating the sandboxed Python enviroment, which
includes the necessary libraries as well as a sandboxed Python interpreter. If you do not
do this step then the code will not run as it depends on the Python interpreter found in
`./virtual`

Next, you can start the Python web-server via:
```python
python runserver.py
```
By default, the web-server runs on `port 5000`. You can change the port value in `gor0x/settings/config.py`

To begin using the IGA, point your web browser to `http://localhost:5000`

**Note**: You will see a `ConnectionError: Error 111 connecting localhost:6379. Connection refused.` if you do not
have the `redis-server` running before running `python runserver.py`


### Project Structure
* `./bin` contains:
  * A Redis configuration file
  * All of the MIDI files that I had access to, which can be found in `./bin/midi`
  * `populate_cache.py`, which is now deprecated and should not be used
  * `install_fluid_synth.sh`, which is _supposed_ to install MIDI on OS X Mavericks since MIDI is not installed by default on Mavericks, however, I and many other people still had trouble getting MIDI files to play even after installing it

* `./gor0x` contains:
  * `./ga` - the genetic algorithm, Markov chain, and Redis caching
  * `./server` - the Python web-server, which uses Flask
  * `./static` - the custom JavaScript for this project as well as vendor JavaScript
  * `./templates` - the different Jinja2 templates used to render the HTML


### Installing pip
If you do not have `pip` on your system, then you can install it via `easy_install pip`. If you do not have `easy_install`, then you will need to go here and follow the instructions to install it http://www.pip-installer.org/en/latest/installing.html


All right reserved for ther author and University of Malaya, Semester 1 2014/2015
