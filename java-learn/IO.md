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

There are four buffered stream classes used to wrap unbuffered streams: BufferedInputStream and BufferedOutputStream create buffered byte streams, while BufferedReader and BufferedWriter create buffered character streams.

[Scanning and Formatting]
## Scanning 
Objects of type Scanner are useful for breaking down formatted input into tokens and translating individual tokens according to their data type.（从格式化的读）

## Formatting
Stream objects that implement formatting are instances of either PrintWriter, a character stream class, or PrintStream, a byte stream class（读完输出格式化）


## <a name="2">Exception e</a>



