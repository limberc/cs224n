# CS224n: Natural Language Processing with Deep Learning

### Stanford / Winter 2019

Natural language processing (NLP) is one of the most important technologies of the information age, and a crucial part of artificial intelligence. Applications of NLP are everywhere because people communicate almost everything in language: web search, advertising, emails, customer service, language translation, virtual agents, medical reports, etc. In recent years, Deep Learning approaches have obtained very high performance across many different NLP tasks, using single end-to-end neural models that do not require traditional, task-specific feature engineering. In this course, students will gain a thorough introduction to cutting-edge research in Deep Learning for NLP. Through lectures, assignments and a final project, students will learn the necessary skills to design, implement, and understand their own neural network models. This year, CS224n will be taught for the first time using [PyTorch](https://pytorch.org/) rather than TensorFlow (as in previous years).

### Reference Texts

The following texts are useful, but not required. All of them can be read free online.

- Dan Jurafsky and James H. Martin. [Speech and Language Processing (3rd ed. draft)](https://web.stanford.edu/~jurafsky/slp3/)
- Jacob Eisenstein. [Natural Language Processing](https://github.com/jacobeisenstein/gt-nlp-class/blob/master/notes/eisenstein-nlp-notes.pdf)
- Yoav Goldberg. [A Primer on Neural Network Models for Natural Language Processing](http://u.cs.biu.ac.il/~yogo/nnlp.pdf)
- Ian Goodfellow, Yoshua Bengio, and Aaron Courville. [Deep Learning](http://www.deeplearningbook.org/)

If you have no background in neural networks but would like to take the course anyway, you might well find one of these books helpful to give you more background:

- Michael A. Nielsen. [Neural Networks and Deep Learning](http://neuralnetworksanddeeplearning.com/)
- Eugene Charniak. [Introduction to Deep Learning](https://mitpress.mit.edu/books/introduction-deep-learning)

### Assignments

- Assignment 1 (6%): Introduction to word vectors.
- Assignment 2 (12%): Derivatives and implementation of word2vec algorithm.
- Assignment 3 (12%): Dependency parsing and neural network foundations .
- Assignment 4 (12%): Neural Machine Translation with sequence-to-sequence and attention.
- Assignment 5 (12%): Neural Machine Translation with ConvNets and subword modeling.

### Practical Tips for using Virtual Machines

In developing your deep learning models, you will likely have to leave certain processes, such as Tensorboard and your training script, running for multiple hours. If you leave a script running on a VM and log-off, your process will likely be disrupted. Furthermore, it is often quite nice to be able to have multiple terminal windows open with different processes all visible at the same time, without having to SSH into the same machine multiple different times.

**TMUX**  is a very simple solution to all the problems above.Essentially, TMUX makes it such that in a single SSH session, you can virtually have multiple terminal windows open, all doing completely separate things. Also, you can actually tile these windows such that you have multiple terminal sessions all visible in the same window.

**TMUX Cheatsheet**

1. Start a new session with the default name (an integer) `$ tmux`
2. Start a new session with a user-specified name `$ tmux new -s [name]`
3. Attach to a new session `$ tmux a -t [name]`
4. Switch to a session `$ tmux switch -t [name]`
5. Detach from a session `$ tmux detach OR ctrl - b - d`
6. List sessions `$ tmux list-sessions`
7. Kill a sessions `ctrl - b - x`
8. Split a pane horizontally `ctrl - b - "`

It would have better experience if you are using Mac.

**see/modify which processes you are running**

1. View all processes `$ ps au`
2. To search among processes for those containing the a query, use 
   `$ ps -fA | grep [query] `. For example, to see all python processes run `ps -fA | grep python`.
3. Kill a process `$ kill -9 [PID]`

You can find the PID (or Process ID) from the output of (1) and (2).

To **monitor your normal RAM and CPU usage**, you can use the following command: `$ htop` (Hit `q` on your keyboard to quit.)

To **monitor your GPU memory usage**, you can use the `$ nvidia-smi` command. If training is running very slowly, it can be useful to see whether you are actually using your GPU fully. (In most cases, when using the GPU for any major task, utilization will be close to 100%, so that number itself doesn't indicate an Out of Memory (OOM) problem.) If you want to monitor the GPU process, you could use `$ watch -n 3 nvidia-smi` which refresh the dashboard every 3 seconds. 

However, it may be that **your GPU is running out of memory simply because your model is too large** (i.e. requires too much memory for a single forward and backward pass) to fit on the GPU. In that case, you need to either:

1. Reduce the size of your model to fit on one GPU. This means reducing e.g. the number of layers, the size of the hidden layers, or the maximum length of your sequences (if you're training a model that takes sequences as input). 
2. Lower the batch size used for the model. Note however, that this will have other effects as well. The traditional batch normalization (like the original Batch Normalization in PyTorch or any other frameworks) processing the Batch Normalization in each GPU separately. 