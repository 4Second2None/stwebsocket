# stwebsocket

It's not about the salary, just for fun!!!!

    本代码是基于state_threads实现的websocket客户端和服务端库，整个websocket的建立和数据交互是完全异步进行的，本质上
还是基于事件驱动状态机（EDSM）。EDSM将线性思维分解成一堆回调负担，这是有悖人类的正常思维的。得益于
state_threads，本代码可以在state_threads的线程（协程）中使用。这样就可以以多线程编程的思维写出性能足以和
EDSM相媲美的程序。由于state_threads的线程是用户级线程，所以想要更高效地利用多核，在多进程的模型下运用本库
会达到你想要的效果。别尝试在多线程下引用本库，那是和本代码的设计理念是向悖的。
    限制：
        1、所有I/O操作必须使用state_threads提供的API，否则会破坏其优异的异步框架，而导致阻塞，和线程调度方面的
    问题。这也暗示了一个问题比如你想在用了我这份代码后，又想添加http接口，那么其它第三方库基本不可用，你必须
    在state_threads的基础上实现http接口（谁叫你用人家的东西呢！你得遵守标准，既然搞C语言开发就别怕造轮子）。
        2、目前只支持linux系统，虽然state_threads有针对windows的移植，但是我不敢用（不要问我为什么）。
        3、state_threads的API不够丰富。比如对文件的异步读写等等，当然不排除我自己fork它的代码，然后自己添加一些API（先mark一下，哈哈）。
        4、由于没有将websocket服务端的握手过程中的socket的监听和接受连接在逻辑上分开，所以现在服务端暂时不支持多进程的模式（已经完善）

    优点：
        利用multi-thread的简单优雅范式胜过传统异步回调的复杂晦涩实现，又利用EDSM的性能和解耦架构避免了multi-thread在系统上的开销和暗礁。
        融合multi-thread和EDSM两者的优点了（哈哈）。
