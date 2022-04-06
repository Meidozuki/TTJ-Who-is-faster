MNIST+MLP(1 hidden layer)
1st time
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

2nd time

| |No.| epoch | batch_size | learning_rate | optimizer | time |
|-|-|-|-|-|-|-|
|tf + JIT |1| 20 | 32 | 1e-3 | Adam |28.4s|
| |2|"|"|"|"|28.1s|
|tf without JIT |1|"|"|"|"|25.4s|
| |2|"|"|"|"|26.2s|
|pytorch | 1 |"|"|"|"|83s|
| |2|"|"|"|"|80s|
|jittor | 1 |"|"|"|"|69s|
| |2|"|"|"|"|67s|

ResNet50+CIFAR10

| |No.| epoch | batch_size | learning_rate | optimizer | time |
|-|-|-|-|-|-|-|
| base on <br> GTX3090 |-| 5 | 32 | 1e-3 | RMSProp |-|
|tensorflow  |1| "|"|"|"|3'10"|
| |2|"|"|"|"|2'42"|
|pytorch | 1 |"|"|"|"|3'16"|
| |2|"|"|"|"|3'17"|
|jittor | 1 |"|"|"|"|3'48"|
| |2|"|"|"|"|3'50"|
|tensorflow \* |1| "|"|"|"|3'26"|
|pytorch \* | 1 |"|"|"|"|3'2"|


| |No.| steps | batch_size | learning_rate | optimizer | time |
|-|-|-|-|-|-|-|
| base on <br>GTX1070Ti |-| 1000 | 8 | 1e-3 | RMSProp |-|
|tensorflow 2.6.3  |1| "|"|"|"|32s|
| |2|"|"|"|"|32s|
|pytorch 1.11.0 | 1 |"|"|"|"|55s|
| |2|"|"|"|"|54s|
|jittor 1.3.1 | 1 |"|"|"|"|54s|
| |2|"|"|"|"|53s|