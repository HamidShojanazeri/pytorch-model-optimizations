# pytorch-model-optimizations 

## High level ideas

- Cloud vs Edge -- many prefer edge to save cloud costs and avoid network latency. 
- Taget hardware -- figure out ideal hardware based on the model size/ available optimizations for HW, Cost
- Choose a path to optimize model -- it's a tarade of between the effort and perfromance gain/ needs
- Use Pytorch out-of-box techniques, Quantizaiton (works for CPU), Torchscript (gives you a graph/ remove dependency to Python), Pruning (not very popular)
- Use model compilers -- ORT, IPEX, TensorRT, TVM


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

### ML Hardware Startups

![image](https://user-images.githubusercontent.com/9162336/162549770-4e55d378-97b8-4816-80e2-ffe4872f137d.png)
https://huyenchip.com/2021/09/07/a-friendly-introduction-to-machine-learning-compilers-and-optimizers.html
