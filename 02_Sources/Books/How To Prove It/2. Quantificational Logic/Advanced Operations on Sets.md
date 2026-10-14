# Keywords
- Index Family
- Index Set

# Transition to Advanced Set Notation
Now that we are familiar with *[[Quantificational Logic#Quantifiers|quantifiers]]*, we can discuss more advanced topics in set theory. For example, we previously defined a set this way, lets say $S$ is the set of all perfect squares:
$$S={\{ x^2\vert x\in \mathbb{N}\}}$$
We can now define the same set this way:
$$S=\{ x \; \vert \;\exists n\in\mathbb{N}\,(n^2=x) \}$$
# Indexed Family
Let's say we want to define a set for the first 100 prime numbers. We can define the $i$-th prime number as $p_{i}$ , then the set would be $P=\{ p_{1}, p_{2}, \dots,p_{100} \}$. Another way to say this is to define $P$ as: 
$$P={\{ p_{i} \;\vert\; i\in I\}}$$
Where:
$$I=\{ i\in\mathbb{N}\;\vert\; 1\leq i\leq 100 \}$$
Here, $P$ is called the *indexed family* and $I$ is called the *index set*. The *index* does not have to be numbers. You can think of the index as a "key" like in a hash map.
>[!note]
>In general, any *indexed family*:
>$$A= \{ x_{i} \;\vert\; i\in I \} \;\text{ can also be defined as } \; A=\{ x \;\vert\; \exists i\in I(x=x_{i}) \}$$
>And consequently:
>$$x\in \{ x_{i} \;\vert\; i\in I\} \equiv \exists i\in I(x=x_{i})$$

