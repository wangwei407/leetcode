# [Basic I/O](#1)
# [Exception e](#2)
## <a name="1">Basic I/O</a>
[Byte Streams](https://docs.oracle.com/javase/tutorial/essential/io/bytestreams.html)
* FileInput/OutputStream (8bits) read()/write()

[Character Streams](https://docs.oracle.com/javase/tutorial/essential/io/charstreams.html)
* FileReader/Writer (16bits) read()/write()
* line oriented I/O BufferedReader/PrintWriter  readline()/println()  

[Buffered Streams]  ()  
Most of the examples we've seen so far use unbuffered I/O. This means each read or write request is handled directly by the underlying OS. This can make a program much less efficient, since each such request often triggers disk access, network activity, or some other operation that is relatively expensive.
To reduce this kind of overhead, the Java platform implements buffered I/O streams. Buffered input streams read data from a memory area known as a buffer; the native input API is called only when the buffer is empty. Similarly, buffered output streams write data to a buffer, and the native output API is called only when the buffer is full.

## <a name="2">Exception e</a>



