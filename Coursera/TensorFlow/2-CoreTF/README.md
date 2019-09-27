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
    print(c)     # Debug output
    # Build
    with tf.Session() as sess:
        result = sess.run(c)
        print(result)
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
        print(z.eval())      # [4, 7, 10]
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
        print(a1)            # [4, 7, 10]
        print(a3)            # [-1, 3, 11]
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
    print(x - y)

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
            ```python
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
        print(y.eval())      # [5, 6]
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
        print(y.eval())      # [[3, 5], [7, 4], [6, 8]]
    ```
    ```python
    import tensorflow as tf
    x = tf.constant([[3, 5, 7], [4, 6, 8]])
    y = tf.reshape(x, [3, 2])[1, :]
    with tf.Session() as sess:
        print(y.eval())      # [7, 4]
    ```

### Variables

> [![](https://img.youtube.com/vi/8REbfWn5mog/0.jpg)](https://youtu.be/8REbfWn5mog)

* A variable is a tensor whose value is initialized and then typically changed as the program runs
    ```python
    def forward_pass(w, x):
        return tf.matmul(w, x)
    
    def train_loop(x, niter=5):
        with tf.variable_scope('model', reuse=tf.AUTO_REUSE):
            # Create variable, specifying how to initialize and whether it can be tuned
            w = tf.get_variable('weights', 
                shape=(1, 2),   # 1x2 matrix
                initializer=tf.truncated_normal_initializer(),
                trainable=True)
        preds = []
        for k in xrange(ninter):
            # "Training loop" of 5 updates to weights
            preds.append(forward_pass(w, x))
            w = w + 0.1     # gradient update
        return preds
    
    with tf.Session() as sess:
        # Multiplying [1, 2] x [2, 3] yields a [1, 3] matrix
        preds = train_loop(tf.constant([[3.2, 5.1, 7.2], [4.3, 6.2, 8.3]]))     # 2x3 matrix
        # Initialize all variables
        tf.global_variables_initializer().run()
        for i in xrange(len(preds)):
            # Print [1, 3] matrix at each of the 5 iterations
            print('{}:{}'.format(i, preds[i].eval()))
    ```
* Placeholders allows you to feed in values, such as by reading from a text file
    ```python
    import tensorflow as tf

    a = tf.placeholder('float', None)
    b = a * 4
    print(a)     # Tensor("Placeholder:0", dtype=float32)
    with tf.Session() as sess:
        print(sess.run(b, feed_dict={a: [1, 2, 3]}))
    ```

### Discussion Prompt: Variables and Placeholder

What is the difference between a placeholder and a variable? Consider a web application (or some other type of program that you are familiar with). How is the difference between placeholders and variables captured?

---
## Lab 1: Writing Low-level TensorFlow Programs

> [![](https://img.youtube.com/vi/JA5ge2l-sjw/0.jpg)](https://youtu.be/JA5ge2l-sjw)

* Please follow the details in [here](./Lab-1.md)

### Lab Solution

> [![](https://img.youtube.com/vi/MhMwKdVtJSo/0.jpg)](https://youtu.be/MhMwKdVtJSo)

---
## Debugging TensorFlow Programs

> [![](https://img.youtube.com/vi/DWWy_ZyOpCg/0.jpg)](https://youtu.be/DWWy_ZyOpCg) 

* Debugging TensorFlow programs is similar to debugging any piece of software
    * Read error messages
    * Isolate the method in question
    * Send made-up data into the method
    * Know how to solve common problems

### Shape Problems

> [![](https://img.youtube.com/vi/i259g4RTWBE/0.jpg)](https://youtu.be/i259g4RTWBE) 

* Know how to solve common problems
    * Tensor shape
    * Scalar-vector mismatch
    * Data type mismatch
* The most common problem tends to be tensor shape
    ```python
    def some_method(data):
        a = data[:, 0 : 2]
        print(a.get_shape())     # (4, 2)
        c = data[:, 1]
        # c = data[:, 1 : 3]
        print(c.get_shape())     # (4,)
        # assert len(c.get_shape()) == 2
        s = (a + c)
        return tf.sqrt(tf.matmul(s, tf.transpose(s)))
    
    with tf.Session() as sess:
        fake_data = tf.constant([
            [5.0, 3.0, 7.1],
            [2.4, 4.1, 4.8],
            [2.8, 4.2, 5.6],
            [2.9, 8.3, 7.3]
        ])
        print sess.run(some_method(fake_data))
    ```
* Shape problems also happen because of batch size or because you have a scalar when a vector is needed (or vice versa)
    ```python
    n_input = tf.constant([3])
    X = tf.placeholder(tf.float32, [None, n_input])
    print(X)
    ...
    fake_data = tf.constant([5.0, 3.0, 7.1])
    ```
    * Output
        ```python
        ValueError: Cannot feed value of shape (3,)
        Tensor("Placeholder_4:0", shape=(?, 3), dtype=float32)
        ```
* Shape problems can often be fixed using
    * `tf.reshape()`
    * `tf.expand_dims()`
    * `tf.slice()`
    * `tf.squeeze()`

### Fixing Shape Problems

> [![](https://img.youtube.com/vi/DSKyPLcHM2A/0.jpg)](https://youtu.be/DSKyPLcHM2A) 

* `tf.expane_dims()` inserts a dimension of 1 into a tensor's shape
    ```python
    x = tf.constant([
        [3, 2], [4, 5], [6, 7]
    ])
    print('x.shape', x.shape)
    expanded = tf.expand_dims(x, 1)
    print('expanded.shape', expanded.shape)

    with tf.Session() as sess:
        print('expanded:\n', expanded.eval())
    ```
    * Output
        ```python
        x.shape (3, 2)
        expanded.shape (3, 1, 2)

        expanded:
        [[[3 2]]
         [[4 5]]
         [[6 7]]]
        ```
* `tf.slice()` extracts a slice from a tensor
    ```python
    x = tf.constant([[3, 2], [4, 5], [6, 7]])
    print('x.shape', x.shape)
    sliced = tf.slice(x, [0, 1], [2, 1])
    print('sliced.shape', sliced.shape)

    with tf.Session() as sess:
        print('sliced:\n', sliced.eval())
    ```
    * Output
        ```python
        x.shape (3, 2)
        sliced.shape (2, 1)

        sliced:
        [[2]
         [5]]
        ```
* `tf.squeeze()` removes dimensions of size 1 from the shape of a tensor
    ```python
    t = tf.constant([[[1], [2], [3], [4]], [[5], [6], [7], [8]]])
    with tf.Session() as sess:
        print('t')
        print(sess.run(t))
        print('t squeezed', sess.run(tf.squeeze(t)))
    ```
    * Output
        ```python
        t
        [[[1]
          [2]
          [3]
          [4]]
          
         [[5]
          [6]
          [7]
          [8]]]
        t squeezed
        [[1 2 3 4]
         [5 6 7 8]]
        ```

### Data Type Problems

> [![](https://img.youtube.com/vi/AKsVUh3fezE/0.jpg)](https://youtu.be/AKsVUh3fezE) 

* Another common problm is **data type**
    ```python
    ValueError: Tensor conversion requested dtype float32 for Tensor with dtype int32: 'Tensor("Const_34:0", shape=(2, 3), dtype=int32)'
    ```
* The reason is because we are mixing types
    ```python
    def some_method(a, b):
        s = (a + b)     # Adding a tensor of floats to a tensor of ints won't work
        return tf.sqrt(tf.matmul(s, tf.transpose(s)))
    
    with tf.Session() as sess:
        # A tensor of floats
        fake_a = tf.constant([
            [5.0, 3.0, 7.1],
            [2.3, 4.1, 4.8]
        ])
        # A tensor of ints
        fake_b = tf.constant([
            [2, 4, 5],
            [2, 8, 7]
        ])
        print(sess.run(some_method(fake_a, fake_b)))
    ```
    * One soluton is to do a cast with `tf.cast()`
        ```python
        def some_method(a, b):
            b = tf.cast(b, tf.float32)
            s = (a + b)     
            return tf.sqrt(tf.matmul(s, tf.transpose(s)))
        ```
        * Output
            ```python
            [[ 15.63361835  16.04929924]
             [ 16.04929924  17.43960953]]
            ```

### Debugging Full Programs

> [![](https://img.youtube.com/vi/5KKUDBais14/0.jpg)](https://youtu.be/5KKUDBais14) 

* To debug full-blown programs, there are three methods
    * `tf.Print()`
    * `tfdbg`
    * TensorBoard
* Change logging level from `WARN`
    ```python
    tf.logging.set_verbosity(tf.logging.INFO)
    ```
* `tf.Print()` can be used to log specific tensor values
    ```python
    import tensorflow as tf

    def some_method(a, b):
        b = tf.cast(b, tf.float32)
        s = (a / b)     # oops! NaN
        print_ab = tf.Print(s, [a, b])
        s = tf.where(tf.is_nan(s), print_ab, s)
        return tf.sqrt(tf.matmul(s, tf.transpose(s)))
    
    with tf.Session() as sess:
        fake_a = tf.constant([[5.0, 3.0, 7.1], [2.3, 4.1, 4.8]])
        fake_b = tf.constant([[2, 0, 5], [2, 8, 7]])
        print(sess.run(some_method(fake_a, fake_b)))
    ```
    * Execution: `python xyz.py`
    * Output
        ```python
        [[  nan            nan]
         [  nan     1.43365264]]
        ```
    * More info: https://www.tensorflow.org/programmers_guide/debugger
* TensorFlow has a dynamic, interactive debugger (no easy way to use it from Datalab currently)
    ```python
    import tensorflow as tf
    from tensorflow.python import debug as tf_debug

    def some_method(a, b):
        b = tf.cast(b, tf.float32)
        s = (a / b)     # oops! NaN
        return tf.sqrt(tf.matmul(s, tf.transpose(s)))
    
    with tf.Session() as sess:
        fake_a = tf.constant([[5.0, 3.0, 7.1], [2.3, 4.1, 4.8]])
        fake_b = tf.constant([[2, 0, 5], [2, 8, 7]])

        sess = tf_debug.LocalCLIDebugWrapperSession(sess)
        sess.add_tensor_filter('has_inf_or_nan', tf_debug.has_inf_or_nan)
        print(sess.run(some_method(fake_a, fake_b)))
    ```
    * Execution: `python xyz.py --debug`
* Use TensorFlow debugger to step through code

### Demo: Debugging TensorFlow Programs

> [![](https://img.youtube.com/vi/gw6MPSIujdw/0.jpg)](https://youtu.be/gw6MPSIujdw)
> [![](https://img.youtube.com/vi/EjzW7zzEdWw/0.jpg)](https://youtu.be/EjzW7zzEdWw)

* Follow along with the code notebook here: https://github.com/GoogleCloudPlatform/training-data-analyst/blob/master/courses/machine_learning/deepdive/03_tensorflow/debug_demo.ipynb

---
## Module Quiz

1. What is TensorFlow? (choose all that apply)
    * A. TensorFlow is an open-source high-performance library for numerical computation that uses directed graphs
    * B. TensorFlow is open source
    * C. TensorFlow is used exclusively to build Machine Learning models
    > Answer: A. B.
2. True or False: When you run a TensorFlow graph (like a + b), you immediately get the output of the graph (the sum of a and b)
    * True - but only if you have tf.eager mode enabled
    * False - TensorFlow always builds the graph but does not execute it
    > Answer: True.
3. What do nodes in a TensorFlow graph represent?
    * A. Mathematical operations
    * B. Arrays of data
    * C. Machine Learning
    * D. All of the above
    > Answer: A.
4. What is a tensor?
    * A. A n-dimensional array of data (generalization of a vector)
    * B. A hyperparameter set before model training
    * C. A different machine learning model type
    > Answer: A.
5. True or False: You can only run TensorFlow on Google Cloud
    * True
    * False
    > Answer: False.
6. The iterative process where a TensorFlow model can crowdsource and combine model feedback from individual users is called what?
    * A. Federated learning
    * B. TensorFlow learning
    * C. Distributed learning
    > Answer: A.
7. What is the high level API that allows for distributed training in TensorFlow?
    * A. `tf.estimator`
    * B. `tf.losses`
    * C. `tf.dist_train`
    * D. `tf.evaluate`
    > Answer: A.
8. How do you run a TensorFlow graph?
    * A. Call `run()` on a `tf.Session`
    * B. TensorFlow graphs are ran automatically
    * C. Call `execute()` on a `tf.Session`
    > Answer: A.
9. Why would you call tf.summary.FileWriter?
    * A. To write out the trained ML model output into a file for distribution
    * B. To output statistics and visualize them in a tool like TensorBoard
    * C. To output the graph in a human-readable format for sharing
    > Answer: B.
10. What is the shape of `tf.constant([2, 3, 5])`?
    * A. It's a scalar so it would be (3)
    * B. It's a vector so it would be (3)
    * C. It's a vector so it would be (1,3)
    * D. It's a scalar so it would be ( )
    > Answer: B.
