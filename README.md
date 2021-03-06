# JXmodem

## Introduction

This library is a port of Georges Menie's Xmodem routines to Java, adapted to use Java classes (particularly streams) and with support for XModem-1k.

The original C code can be found here: https://www.menie.org/georges/embedded/

The library is written in pure Java. It supports Xmodem, Xmodem-CRC, and XModem-1k. For Xmodem-1k and Xmodem-CRC, CRC calculation is performed via a pre-calculated lookup table.

The library has been tested for accuracy using the `sx` and `rx` programs both on the same machine and over a local area network. Further testing under different conditions is both welcome and encouraged.

## Add as a dependency

Add the following dependency to your projects `pom.xml` file:

```xml
<dependency>
    <groupId>io.github.neonSonOfXenon.JXmodem</groupId>
    <artifactId>JXmodem</artifactId>
    <version>0.1a</version>
</dependency>

```

## Usage

Usage is fairly simple. All you need is an InputStream and OutputStream to initialize JXmodem:

```Java
JXmodem xm = new JXmodem(someInputStream, someOutputStream);
```

From there, you have a host of functions for simple sending and receipt of byte arrays, strings, and files.

### Sending and receiving byte arrays

Sending a byte array is as easy as

```Java
byte[] bs = "this is an example string that will be turned into a byte array".getBytes();
boolean success = xm.send(bs); // returns true if the send succeeded
```

The method `send(byte[] data, int offset, int length)` also exists for sending subsets of byte arrays.

To receive a byte array, simply do

```Java
byte[] bs = xm.receive();
```

### Sending and receiving strings

Strings may be sent using the `sendString()` method:

```Java
String s = "this is an example string that will remain a string";
boolean success = xm.sendString(s); // returns true if the send succeeded
```

You also have the option to specify a character set for the string via `sendString(String message, String charset)`.

String receipt can be done like so:

```Java
String s = xm.receiveString();
```

Just like sending, you can specify a charset for encoding the string with `recieveString(String charset)`.

### Sending and receiving files

File transfers are possible through `sendFile()` and `receiveFile()`. These methods handle reading and writing the files to and from local storage. You just need to provide a valid filepath.

```Java
// sending a file
String outFilename = "path/to/file.xyz";
boolean sendSuccess = xm.sendFile(outFilename); // returns true if the send succeeded

// receiving a file
String inFilename = "path/to/newFile.xyz";
boolean receiveSuccess = xm.receiveFile(inFilename); // returns true if the file was received 
                                                     // and saved successfully
```

## Still to do

The following is a list of improvements still needed:

* Clean up debugging printouts
* Generate Javadoc
