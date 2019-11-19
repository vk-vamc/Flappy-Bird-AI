# Flappy Bird AI

To run the cloned project. Navigate into the diirectory it is in and then open command prompt and run the following commmands.

<code>
pip install requirements.txt |
python flappy_bird.py
<code>

Using learning algorithms, we want to allow AI player to do a training set with different definitions of states, and learn the flappy bird world.After the training set, we want the bird to successfully continue playing as long as we want without any hit.

Our project mainly consists of 2 phases:

1. Creating the &quot;Flappy Bird&quot; game (so as to tweak it properly for the AI)
2. Incorporate the neat algorithm into it.

1) **Flappy Bird Game:**

The objective is to direct a flying bird who moves continuously to the right, between sets of ​ Mario-like pipes​. If the player touches the pipes, they ​ lose​. The bird briefly flaps upward each time that the player taps the screen; if the screen is not tapped, the bird falls because of ​ gravity​; each pair of pipes that he navigates between earns the player a single ​ point

We create the simple game by using the &quot;pygame&quot; python package. Although, no user will be able to play it, the AI can play and learn from it.

**2) Incorporation of the algorithm:**

We incorporate the NEAT algorithm using the &quot;neat-python&quot; package.

It evolves a basic neural network and changes the values of the weights, removes and randomly adds other nodes. The reason it does this is to try to find a topology (kind of an architecture) for the neural network that works best for the given situation. If the situation is complex it adds nodes else it doesn&#39;t make it complex. If we have a basic neural network that is favorable NEAT retains it.

Things needed to give the NEAT algorithm:

1. **Inputs:**

These are the inputs we give to the neural network representing each bird irrespective of the species. We give the network the position of the bird and the distance between the next-coming top pipe and the bottom height.

2. **Output:**

We have only one operation to perform whether to jump or not (only one node for the output).

3. **Activation Function**:

We are only going to choose the activation function for the output neuron and let NEAT choose the activation function for the hidden layers.

4. **Population Size:**

This is the number of sample birds taken at the beginning of every generation

5. **Fitness Function:**

This is by far the most important part in the algorithm. It quantifies how the birds are going to grow and eventually get better. It evaluates how good the birds are. In our case it is the distance traversed by the bird.

6. **Max Generations:**

It is the number of generations after which you terminate the process.

**Default Genome:** All our population members are called genomes. They have 2 attributes nodes and genes(edges).

The following are the attributes used:

_fitness\_criterion:_ This is simply a function which determines the best bird. (It can take values of min, mean, max)

_fitness\_threshold:_ if any of the birds reach this value, the program terminates.

_pop\_size:_ population size

_reset\_on\_extinction:_ It is a Boolean value, which when true resets a species with random weights upon its extinction.

# Node activation options
_activation\_default_ : the activation function for the output neuron
_activation\_mutate\_rate_ : mutation probability
_activation\_options_ : The set of activation functions from which NEAT chooses based on mutate rate



_Node bias options:_ Initial bias values
bias\_init\_mean
bias\_init\_stdev
bias\_max\_value

bias\_min\_value
bias\_mutate\_power
bias\_mutate\_rate
bias\_replace\_rate

_Connection weight options_
weight\_init\_mean
weight\_init\_stdev
weight\_max\_value
weight\_min\_value
weight\_mutate\_power
weight\_mutate\_rate
weight\_replace\_rate

_Connection add/remove rates:_ how likely we are to add /remove a connection
conn\_add\_prob
conn\_delete\_prob

_Node add/remove rates:_ how likely we are to add /remove a node
node\_add\_prob
node\_delete\_prob

_Network parameters:_
num\_hidden              = 0
num\_inputs              = 3
num\_outputs             = 1

_max\_stagnation :_ how many generations we go until we go without extinction.



**Mutation:**

In NEAT, mutation can either mutate existing connections or can add new structure to a network. If a new connection is added between a start and end node, it is randomly assigned a weight.

If a new node is added, it is placed between two nodes that are already connected. The previous connection is disabled (though still present in the genome). The previous start node is linked to the new node with the weight of the old connection and the new node is linked to the previous end node with a weight of 1. This was found to help mitigate issues with new structural additions

**Crossover:**

Crossing over the genomes of two neural networks could result in networks that are horribly mutated and non-functional.

NEAT tackles this issue through the usage of historical markings (as seen above). By marking new evolutions with a historical number, when it comes time to crossover two individuals, this can be done with much less chance of creating individuals that are non-functional. Each gene can be aligned and (potentially) crossed-over. Each time a new node or new type of connection occurs, a historical marking is assigned, allowing easy alignment when it comes to breed two of our individuals.