# Pytorch model optimizations for inference
## Find the buttleneck
Running efficinet DL model boild down to three components:

- Compute : time spent on GPU running actual FLOPS
- Memory :time spend to trnasder data from CPU to GPU
- Overhead : everythings else:
Great [blog](https://horace.io/brrr_intro.html) from Horace.

## High level ideas

- Cloud vs Edge -- many prefer edge to save cloud costs and avoid network latency. 
- Taget hardware -- figure out ideal hardware based on the model size/ available optimizations for HW, Cost
- Choose a path to optimize model -- it's a tarade of between the effort and perfromance gain/ needs
- Use Pytorch out-of-box techniques, Quantizaiton (works for CPU), Torchscript (gives you a graph/ remove dependency to Python), Pruning (not very popular)
- Use model compilers --TensorRT, TVM 
- OR offerings by IPEX and OnnxRuntime


#### Target hardware 

To framework on a hardware, hardware vendor need to support that framework. Hardware companies provide kernels for a number of frameworks for example Nvidia has Cuda and CuDNN. 

A fundamental challenge is that different hardware types have different memory layouts and compute primitives

Supported Hardwares for Pytorch CPU/ GPU/TPU/Inferentia/Trainum

Compute primitives

CPU : Scalar, vector
GPU : one dimensional Vector, Two dimensional (Tensor cores) A100, V100, T4
TPU : Two dimensional vectors

Memory layouts shown below, play an important role in the perfromance. 

<img width="150", height="150" alt="Screen Shot 2022-04-08 at 5 57 49 PM" src="https://user-images.githubusercontent.com/9162336/162550272-1f509587-476e-4fbd-9409-2b6faa8eb443.png">

[TVM Paper](https://arxiv.org/pdf/1802.04799.pdf)

##### IRs (Intermediate Representations)

Frameworks do not target many different compilers instead they provide IR as bridge between framework and hardware, then hardware compaines take the IR and compile (lower) it for their chip, machine code.  Compiler take the IR, generate high level and low level code using codegen (mostly LLVM)
