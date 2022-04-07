I've tried MLP and Resnet50 model with tensorflow, pytorch and jittor. For me, I'd like to find out which one can train the model faster.  

The result is not obvious, maybe it's because the model used is not big enough, or maybe it depends on PC.

###  MLP(1 hidden layer,512 units) on MNIST dataset

Table 1: I run an epoch warmup and then meassure the total time of 20 epochs. 

| |No.| epoch | batch_size | learning_rate | optimizer | time | memory |
|-|-|-|-|-|-|-|-|
| base on GTX3090 |-| 20 | 32 | 1e-3 | Adam |-|-|
|tensorflow 2.6.0 |1|"|"|"|"|30s|1.2G|
| no JIT prefetch4 |2|"|"|"|"|30s|1.2G|
| |3|"|"|"|"|30s|1.2G|
|pytorch 1.9.1 | 1 |"|"|"|"|48s|1.5G|
| worker4 |2|"|"|"|"|48s|1.5G|
| |3|"|"|"|"|47s|1.5G|
|jittor 1.3.1 | 1 |"|"|"|"|26s|0.77G|
| worker4 |2|"|"|"|"|25s|0.77G|
| |3|"|"|"|"|25s|0.77G|


### ResNet50 on CIFAR10 dataset

This time I do not track GPU memory usage, cauz when initialized, torch/ jittor allocated 1.9G/1.0G only, but when running they actually demands more memory that differs from nvidia-smi - Processes - GPU Memory Usage. Maybe I need to find another way to track it.

Table 3: test on GTX3090
| |No.| epoch | batch_size | learning_rate | optimizer | time |
|-|-|-|-|-|-|-|
| base|-| 5 | 32 | 1e-3 | RMSProp |-|
|tensorflow  |1| "|"|"|"|3'10"|
| |2|"|"|"|"|2'42"|
|pytorch | 1 |"|"|"|"|3'16"|
| |2|"|"|"|"|3'17"|
|jittor | 1 |"|"|"|"|3'48"|
| |2|"|"|"|"|3'50"|
|tensorflow \* |1| "|"|"|"|3'26"|
|pytorch \* | 1 |"|"|"|"|3'2"|

[\*] When I submitted, it collided with another different task. 

Table 4: test on GTX1070Ti
| |No.| steps | batch_size | learning_rate | optimizer | time |
|-|-|-|-|-|-|-|
| Windows10 env |-| 1000 | 8 | 1e-3 | RMSProp |-|
|tensorflow 2.6.3  |1| "|"|"|"|32s|
| |2|"|"|"|"|32s|
|pytorch 1.11.0 | 1 |"|"|"|"|37s|
| |2|"|"|"|"|35s|
|jittor 1.3.1 | 1 |"|"|"|"|45s|
| |2|"|"|"|"|45s|
|WSL2 env|-|1000|8|1e-3|RMSProp|-|
|pytorch 1.11.0 | 1 |"|"|"|"|55s|
| |2|"|"|"|"|54s|
|jittor 1.3.1 | 1 |"|"|"|"|54s|
| |2|"|"|"|"|53s|

## Result
It seems that all the three do not differ significantly from others. Emmm...