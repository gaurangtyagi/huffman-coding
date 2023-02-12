<h1 align='center'> Huffman Zipper</h1>
<h3 align='center'> Yet another file compressor/decompressor, using a C++ huffman-coding algorithm implementation.</h3>
<img center='align' src='https://cdn.shortpixel.ai/client/q_glossy,ret_img,w_1550/https://itpack.be/wp-content/uploads/2019/06/Naamloos.png'/>



We use **Huffman's algorithm** to construct **a tree** that is used for data compression. 
We assume that each character has an associated weight equal to the number of times the character occurs in a file,
When compressing a file we'll need to calculate these weights.

## Huffman Coding Algorithm Description

Huffman's algorithm assumes that we're building a single tree from a group (or forest) of trees. 
Initially, all the trees have a single node with a character and the character's weight. 
Trees are combined by picking two trees, and making a new tree from the two trees. 
This decreases the number of trees by one at each step since two trees are combined into one tree.

### Algorithm Steps:

1. Begin with a forest of trees. All trees are one node, with the weight of the tree equal to the weight of the character in the node. 
Characters that occur most frequently have the highest weights. Characters that occur least frequently have the smallest weights.
Repeat this step until there is only one tree.

2. Choose two trees with the smallest weights, call these trees T1 and T2. Create a new tree whose root has a weight equal to the sum of the weights T1 + T2 and whose left subtree is T1 and whose right subtree is T2.

3. The single tree left after the previous step is an optimal encoding tree.

<p align='center'><img src='https://upload.wikimedia.org/wikipedia/commons/d/d8/HuffmanCodeAlg.png'/></p>

---

## Our Implemetation of Algorithm

There are two parts to an implementation: a compression program and an un-compression/decompression program. 
You need both to have a useful compression utility. We'll assume these are separate programs, but they share many classes, functions, modules, code or whatever unit-of-programming you're using. 

- We'll call the program that reads a regular file and produces a compressed file the **compression or huffing program**.  
- The program that does the reverse, producing a regular file from a compressed file, will be called the **uncompression or un-huffing program**.


### Main Data Structures Used
- Two **unordered maps**, one for the character and coding pairs and another for the character and the frequency or number of times repeated.
- One **priority queue** to apply the minimum heap minimum extraction property in the tree construction algorithm.


### File Header

You must store some initial information in the compressed file that will be used by the uncompression/un-huffing program (the tree basically). There are several alternatives for storing the tree:

- Store the character counts at the beginning of the file. You can store counts for every character, or counts for the non-zero characters. If you do the latter, you must include some method for indicating the character, e.g., store character/count pairs.

- You could use a "standard" character frequency, e.g., for any English language text you could assume weights/frequencies for every character and use these in constructing the tree for both compression and uncompression.

- You can store the tree at the beginning of the file. One method for doing this is to do a pre-order traversal, writing each node visited. You must differentiate leaf nodes from internal/non-leaf nodes. One way to do this is write a single bit for each node, say 1 for leaf and 0 for non-leaf. For leaf nodes, you will also need to write the character stored. For non-leaf nodes there's no information that needs to be written, just the bit that indicates there's an internal node.



## References

*1. [Huffman coding, from WikiWorld](https://www.wikiwand.com/en/Huffman_coding)*

*2. Thomas H. Cormen, Charles E. Leiserson, Ronald L.Rivest, Clifford Stein “Introduction to Algorithms 3rd Edition - Thomas H. Cormen, Charles E. Leiserson, R”*

*3. Weiss, Mark Allen. “Data structures and algorithm analysis in Java." Addison-Wesley Long-man Publishing Co., Inc., 1998.*

---

<h3 align='center'> Made with :heart:</h3>
