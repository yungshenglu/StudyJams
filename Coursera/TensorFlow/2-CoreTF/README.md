# Core TensorFlow

We will introduce you to the core components of TensorFlow and you will get hands-on practice building machine learning programs. You will compare and write lazy evaluation and imperative programs, work with graphs, sessions, variables, as finally debug TensorFlow programs.

## Introduction

> [![](https://img.youtube.com/vi/ocp82KmRvxA/0.jpg)](https://youtu.be/ocp82KmRvxA)

* Learn how to
    * Write lazy evaluation and imperative programs
    * Work with graphs, sessions, and variables
    * Visualize TensorFlow graphs
    * Debug TensorFlow programs

---
## What is TensorFlow?

> [![](https://img.youtube.com/vi/06zoAI3JdZM/0.jpg)](https://youtu.be/06zoAI3JdZM)

* TensorFLow is an *open-source* high-performance library for numerical computation that uses directed graphs
* A tensor is an N-dimensional array of data
    * Rank 0 Tensor: scalar
    * Rank 1 Tensor: vector
    * Rank 2 Tensor: matrix
    * Rank 3 Tensor
    * Rank 4 Tensor

### Benefits of a Directed Graph

> [![](https://img.youtube.com/vi/18uqUZHFNXY/0.jpg)](https://youtu.be/18uqUZHFNXY)

* TensorFlow graphs are protable between different devices
* TensorFlow Lite provides on-device inference of ML models on mobile devices and is available for a variety of hardware
    * Train on cloud
    * Run inference on edge device
* TensorFlow even supports federated learning
* TensorFLow is popular among both deep learning researchers and machine learning engineers

### Quiz

1. TensorFlow is a software framework for:
    * A. Numeric processing
    * B. Neural networks only
    > Answer: A.

---
## TensorFlow API Hierarchy

> [![](https://img.youtube.com/vi/2gT_fnIIjMA/0.jpg)](https://youtu.be/2gT_fnIIjMA)

* TensorFlow toolkit hierarchy
    * TF runs on different hardware
        * e.g., CPU, GPU, TPU, Android
    * C++ API is quite low level
        * Core TensorFlow (C++)
    * Python API gives you full control
        * Core TensorFlow (Python)
    * Components useful when building custom NN models
        * i.e., `tf.layers`, `tf.losses`, `tf.metrics`
    * High-level APPI for distributed training
        * i.e., `tf.estimator`
    * Run TensorFlow at scale with CMLE

### Lazy Evaluation

> [![](https://img.youtube.com/vi/vJ4-j0LSBvA/0.jpg)](https://youtu.be/vJ4-j0LSBvA)

* The Python API lets you build and run Directed Graphs
    ```python
    # Build - Create the graph
    c = tf.add(a, b)
    # Run - Run the graph
    session = tf.Session()
    numpy_c = session.run(c, feed_dict= ...)
    ```
* TensorFlow does lazy evaluation: you need to run the graph to get results
    ```python
    # Run
    a = tf.constant([5, 3, 8])
    b = tf.constant([3, -1, 2])
    c = tf.add(a, b)
    print c     # Debug output
    # Build
    with tf.Session() as sess:
        result = sess.run(c)
        print result
    ```
    * `tf.eager` allows you to execute operations imperatively
    * Unlike with NumPy, TensorFlow `c` is not the actual values

### Discussion Prompt: Importance of an API hierarchy

Which level of the TensorFlow API hierarchy will you tend to work at? Why is it important that the other levels are exposed by the framework?

---
## Graph and Session

> [![](https://img.youtube.com/vi/GY9oNgoa5c4/0.jpg)](https://youtu.be/GY9oNgoa5c4)

* Graph can be processed, compiled, remotely executed, and assigned to devices
    * Data: tensors (N-dimensional arrays)
    * Nodes: operations (ops) on tensors
    * In addition to computation (e.g., add, matmul), constants, variables, logging, and control flow are also Ops
* **Session** allows TensorFlow to cache and distribute comptation
* Execute TensorFlow graphs by calling `run()` on a `tf.Session`
    ```python
    import tensorflow as tf

    x = tf.constant([3, 5, 7])
    y = tf.constant([1, 2, 3])
    z = tf.add(x, y)

    with tf.Session() as sess:
        sess.run(z)     # [4, 7, 10]
    ```

### Evaluating a Tensor

> [![](https://img.youtube.com/vi/b_j0FqC7nVc/0.jpg)](https://youtu.be/b_j0FqC7nVc)

* Evaluating a tensor is a shortcut to calling `run()` on the graph's default session
    ```python
    import tensorflow as tf

    x = tf.constant([3, 5, 7])
    y = tf.constant([1, 2, 3])
    z = tf.add(x, y)

    with tf.Session() as sess:
        print z.eval()      # [4, 7, 10]
    ```
* It is possible to evaluate a list of tensors
    ```python
    import tensorflow as tf

    x = tf.constant([3, 5, 7])
    y = tf.constant([1, 2, 3])
    z1 = tf.add(x, y)
    # Shortcuts to common arithmetic operators
    z2 = x * y
    z3 = z2 - z1

    with tf.Session() as sess:
        # run() accepts a list of tensors
        a1, a3 = sess.run([z1, z3])
        print a1            # [4, 7, 10]
        print a3            # [-1, 3, 11]
    ```
* TensorFlow in **Eager** mode makes it easier to try out things, but is not remommended for production code
    ```python
    import tensorflow as tf
    # Import tf.eager
    from tensorflow.contrib.eager.python import tfe

    # Call exactly once
    tfe.enable_eager_execution()

    x = tf.constant([3, 5, 7])
    y = tf.constant([1, 2, 3])
    print (x - y)

    # Note the value being printed
    tf.Tensor([2, 3, 4], shape=(3,), dtype=int32)   # [2, 3, 4]
    ```

### Visualizing a Graph

> [![](https://img.youtube.com/vi/8Ni5WjfTq7g/0.jpg)](https://youtu.be/8Ni5WjfTq7g)

* You can write the graph out using `tf.summary.FileWriter`
    ```python
    import tensorflow as tf

    # Name the tensors and the operations
    x = tf.constant([3, 5, 7], name='x')
    y = tf.constant([1, 2, 3], name='y')
    z1 = tf.add(x, y, name='z1')
    z2 = x * y
    z3 = z2 - z1

    with tf.Session() as sess:
        # Write the session graph to a summary directory
        with tf.summary.FileWriter('summaries', sess.graph) as writer:
            a1, a3 = sess.run([z1, z3])
    ```
* The graph can be visualized in **TensorBoard**
* You can also write to `gs://` and start TensorBoard from Cloud Shell
    1. Run the following command in Cloud Shell to start TensorBoard:
        ```bash
        $ tensorboard --port 8080 --logdir gs://${BUCKET}/${SUMMARY_DIR}
        ```
    2. To open a new browser window, select `Preview on port 8080` from the `Web Previw` menu in the top-right corner of the Cloud Shell toolbar
        * In the new window, you can use TensorBoard to see the training summary and the visualized network graph
    3. Press `Ctrl-C` to stop TensorBoard in Cloud Shell
        * https://cloud.google.com/ml-engine/docs/dictributed-tensorflow-mnist-cloud-datalab

### Quiz

1. Which of these provides a way to visualize your TensorFlow program as a graph?
    * A. emacs
    * B. TensorBoard
    * C. vim
    > Answer: B.
2. Which of these is a valid way to evaluate a tensor "z"? Assume you have a session named "sess" and it is the default session.
    * A. `sess.run(z)`
    * B. `z.eval()`
    * C. `sess.run([z])`
    > Answer: A. B. C.
3. The mode to evaluate tensors immediately (instead of lazy evaluation) is called:
    * A. Interactive mode
    * B. Eager mode
    * C. This is the default TensorFlow behavior, so there is no special name for it.
    > Answer: B.
4. TensorFlow programs are directed graphs. What are some of the benefits?
    * A. You can write TensorFlow programs using a what-you-see-is-what-you-get (WYSIWYG) user interface
    * B. TensorFlow can optimize the graph by merging successive nodes where necessary
    * C. TensorFlow can insert send and receive nodes to distribute the graph across machines
    > Answer: B. C.

---
## Tensors and Variables

### Tensors

> [![](https://img.youtube.com/vi/xnLwwo4TDTQ/0.jpg)](https://youtu.be/xnLwwo4TDTQ)

* A tensor is an N-dimensional array of data
    * Rank 0: scalar
        * Example: `x = tf.constant(3)`
        * Shape: `()`
    * Rank 1: vector
        * Example: `x = tf.constant([3, 5, 7])`
        * Shape: `(3,)`
    * Rank 2: matrix
        * Example: `x = tf.constant([[3, 5, 7], [4, 6, 8]])`
        * Shape: `(2, 3)`
    * Rank 3: 3D tensor
        * Example: `x = tf.constant([[[3, 5, 7], [4, 6, 8]], [[1, 2, 3], [4, 5, 6]]])`
        * Shape: `(2, 2, 3)`
    * Rank n: nD tensor
        * Example:
            ```python
            x1 = tf.constant([2, 3, 4])
            x2 = tf.stack([x1, x1])
            x3 = tf.stack([x2, x2, x2, x2])
            x4 = tf.stack([x3, x3])
            ```
        * Shape:
            ```
            (3,)
            (2, 3)
            (4, 2, 3)
            (2, 4, 2, 3)
            ```
* Tensors can be sliced
    ```python
    import tensorflow as tf
    x = tf.constant([[3, 5, 7], [4, 6, 8]])
    y = x[:, 1]
    with tf.Session() as sess:
        print y.eval()      # [5, 6]
    ```
    * What would `x[1, :]` do?
        * Answer: `[4, 6, 8]`
    * How about `x[1, 0:2]`?
        * Answer: `[4, 6]`
* Tensors can be reshaped
    ```python
    import tensorflow as tf
    x = tf.constant([[3, 5, 7], [4, 6, 8]])
    y = tf.reshape(x, [3, 2])
    with tf.Session() as sess:
        print y.eval()      # [[3, 5], [7, 4], [6, 8]]
    ```
    ```python
    import tensorflow as tf
    x = tf.constant([[3, 5, 7], [4, 6, 8]])
    y = tf.reshape(x, [3, 2])[1, :]
    with tf.Session() as sess:
        print y.eval()      # [7, 4]
    ```
