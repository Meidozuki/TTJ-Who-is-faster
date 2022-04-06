I've tried MLP and Resnet50 model with tensorflow, pytorch and jittor. For me, I'd like to find out which one can train the model faster.  

The result is not obvious, maybe it's because the model used is not big enough, or maybe it depends on PC.

###  MLP(1 hidden layer,512 units) on MNIST dataset

Table 1: the 1st time I compared the models

| |No.| epoch | batch_size | learning_rate | optimizer | time | memory |
|-|-|-|-|-|-|-|-|
| base |-| 20 | 32 | 1e-3 | Adam |-|-|
|tensorflow 2.6.0 |1|"|"|"|"|36s|1.2G|
|  |2|"|"|"|"|36s|1.2G|
|pytorch 1.9.1 | 1 |"|"|"|"|84s|1.5G|
|  |2|"|"|"|"|87s|1.5G|
| |3|"|"|"|"|85s|1.5G|
|jittor 1.3.1 | 1 |"|"|"|"|82s|0.77G|
| |2|"|"|"|"|78s|0.77G|
| |3|"|"|"|"|79s|0.77G|

Table 2: the 2nd time I compared the models

| |No.| epoch | batch_size | learning_rate | optimizer | time |
|-|-|-|-|-|-|-|
| base |-| 20 | 32 | 1e-3 | Adam |-|
|tf + JIT |1| " | " | " | " |28.4s|
| |2|"|"|"|"|28.1s|
|tf without JIT |1|"|"|"|"|25.4s|
| |2|"|"|"|"|26.2s|
|pytorch | 1 |"|"|"|"|83s|
| |2|"|"|"|"|80s|
|jittor | 1 |"|"|"|"|69s|
| |2|"|"|"|"|67s|

This time I truned on and off the JIT option of tensorflow, to see if JIT would donate speed-up. It seems that JIT takes longer time for the reason that it takes time for JIT to compile, but it happens so fast. (But the following test I exclude the compiling time.)

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
| base |-| 1000 | 8 | 1e-3 | RMSProp |-|
|tensorflow 2.6.3  |1| "|"|"|"|32s|
| |2|"|"|"|"|32s|
|pytorch 1.11.0 | 1 |"|"|"|"|55s|
| |2|"|"|"|"|54s|
|jittor 1.3.1 | 1 |"|"|"|"|54s|
| |2|"|"|"|"|53s|

## Result
It seems that all the three do not differ significantly from others. Emmm...