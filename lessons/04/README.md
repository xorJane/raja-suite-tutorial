# Lesson Four

In this lesson, you will learn to write a loop using the `RAJA::forall` statement,
which is called with the following format:

```
RAJA::forall<EXEC_POLICY>( ITERATION SPACE, LAMBDA);
```

What we mean by `EXEC_POLICY`, `ITERATION SPACE`, and `LAMBDA` are defined in
the following sections.

## Specifying an execution policy

`RAJA::forall` is a loop execution template. To use `RAJA::forall` to execute a
loop, we first need to tell the `RAJA:forall` template *how* the loop will be
executed; for example, will it run on a CPU or GPU? We provide this information
by passing an execution policy type (above, `EXEC_POLICY`), which might specify
that the loop should be executed sequentially, using OpenMP, or using CUDA.

In this example, we will use the `RAJA::loop_exec` policy to execute this loop on
the CPU. In later lessons, we will learn about other policies that allow us to
run code on a GPU.

After specifying our execution policy, we create a `RAJA::forall` method.

## Specifying an iteration space object

The first argument passed to a `RAJA::forall` method is the iteration space
object (`ITERATION SPACE`) that specifies whether the loop will step through a contiguous range,
a strided range, or a list of indices.

We can create a `RAJA::TypedRangeSegment` to describe an iteration space
that is a contiguous sequence of integers `[0, N)`.

```
RAJA::TypedRangeSegment<int>(0, N)
```

## Specifying a lambda

The second and final argument passed to a `RAJA::forall` method specifies the
loop body as a C++ lambda expression (above, `LAMBDA`).

The lambda expression needs to take one argument, the loop index, and has the
following form:

```
[=](int i) { // loop body }
```

Here the `[=]` syntax tells the lambda to capture arguments by value (e.g.
create a copy, rather than a reference).

## Exercise 4

In the file four.cpp, you will see a `TODO` comment where you can add a
`RAJA::forall` loop to initialize the array you allocated in the previous
lesson.

When you have made your changes, compile and run the code in the same way as the
other lessons:

```
$ make four
$ ./bin/four
Address of data:
data[50] = 50
```
