---
layout: post
title: "Unicode and UTF-8: PART I"
description: "Diving into character sets and encodings"
category: Unicode, Data Processing
tags: [Unicode, Data Processing]
---
{% include JB/setup %}
This is the first post aimed at demystifying the concept of Unicode(Character Set) and UTF-8(encoding). 

First of all, it is important to understand what character sets are. <b>A "character set" is a set of characters that are understood by a computer's hardware and software.</b> Every character in a character set is represented by a number. The ASCII character set, for example, uses the numbers 0 through 127 to represent all English characters as well as special control characters. European ISO character sets are similar to ASCII, but they contain additional characters for European languages. 

Consider the ASCII character set. Each character in ASCII character set can be represented uniquely as a number between 0 and 127(inclusive). This means that all the characters in the ASCII character set can be represented in 8 bits(1 byte). This means that ASCII strings(or strings) are capable of representing 128 characters.

The Unicode character set can represent all the characters on earth. This means that unicode character sets can represent text in any language(english, russian, french, chinese, sanskrit and whatever else you can think of). Every character in the Unicode character set is called a code point. 

This is the story about character sets. 

Now what is an encoding? We have seen that the unicode character set can represent every character on the planet. But, text needs to stored, be it in the form of HTML pages on the web, files on the filesystem or data in databases. One thing is certain, that the computer stores data in the form of 0s and 1s. More accuractely, data is stored in the form of bytestreams (obviously, a stream of bytes). OK. It makes sense that ASCII characters, each occupying 1 byte can be easily stored and retrieved from a computer. But what about unicode? How do we store unicode? It turns out that encodings come to the rescue here. <b>An encoding represents a mapping between character sets and bytes.</b> In layman's terms, an encoding understands how to represent a character in terms of bytes(so that it can be stored) and how to recompose a sequence of bytes into the character that they represent(so that we can understand what is written in the form of 0s and 1s when we read it). The encoding responsible for handling Unicode character set is the UTF-8 encoding.

Lets take a step back to look at the whole picture. Unicode is a concept, a set of rules to represent characters. Think of unicode as a concept. Now, data is present in the form of unicode strings(believe it or not, over 50% of the content on the web). Now, we crawl some content from the web(assume that it is a unicode string). We need to store that data on the hardware. For storing the data, we need a bytestream. The UTF-8 encoding <i>encodes</i> this unicode string into a bytestream. Similarly, we need the UTF-8 encoding to <i>decode</i> the bytestream into a unicode string when we read the data from the hardware. We <b>must</b> have both these dual operations done by the UTF-8 encoding. Similary Unicode strings can be encoded and subsequently decoded by the UTF-16 encodings. But it would be nonsensical to encode using UTF-8 and decode using UTF-16 or vice-versa. This also highlights the importance of specifying the encoding of the data. If no encoding is specified we can only guess at what the data might say.     
 
<b>Code Samples</b>
Let's fire up the Python interpreter. The string "¿cómo estás" is in the spanish language and means "how are you".  

	$ python
	Python 2.7.3 (default, Sep 26 2013, 20:03:06) 
	[GCC 4.6.3] on linux2
	Type "help", "copyright", "credits" or "license" for more information.
	>>> s_unicode = u'¿cómo estás'
	>>> type(s_unicode)
	<type 'unicode'>
	>>> s_unicode
	u'\xbfc\xf3mo est\xe1s'

We see that the string s_unicode is a unicode string(The <i>u</i> preceding the quotes is testament to that). When this data is in transit from one machine to another, within an application or elsewhere, it is suitable to think of the data as a unicode string. When this data is stored, it needs to be stored as a bytestream. To convert it to a bytestream, we need to encode it. 

	>>> s_bytestream = s_unicode.encode('utf8')
	>>> s_bytestream
	'\xc2\xbfc\xc3\xb3mo est\xc3\xa1s'
	>>> type(s_bytestream)
	<type 'str'>
	
We see that the string s_bytestream is not a unicode string(notice the missing <i>u</i> preceding the quotes). Furthermore, we see that the type of s_bytestream is a simple Python string. We can not store our unicode string in a file...

	>>> f = open('unicode_string.txt','w')
	>>> f.write(s_bytestream)
	>>> f.close()

A lot of systems provide automatic encoding and decoding with utf8. An example of such a system is MongoDB. Now, lets read the data...

	>>> f = open('unicode_string.txt','r')
	>>> s_bytestream_from_file = f.read()
	>>> f.close()

So, we were able to write and read the spanish language. Lets do some comparisons to understand what s_bytestream_read represents.

        >>> s_bytestream_from_file
        '\xc2\xbfc\xc3\xb3mo est\xc3\xa1s'
        >>> type(s_bytestream_from_file)
        <type 'str'>
        >>> s_bytestream_from_file == s_bytestream
        True
        >>> s_bytestream_from_file == s_unicode
        __main__:1: UnicodeWarning: Unicode equal comparison failed to convert both arguments to Unicode - interpreting them as being unequal
        False

So we see that by default comparing type <i>str</i> and type <i>unicode</i> raises an exception and treats them as unequal. The proper way to compare these strings is as follows...

        >>> s_bytestream_from_file_converted_to_unicode = s_bytestream_from_file.decode('utf8')
        >>> type(s_bytestream_from_file_converted_to_unicode) 
        <type 'unicode'>
        >>> s_bytestream_from_file_converted_to_unicode == s_unicode
        True

This is a complete cycle of unicode and UTF-8 encoding. It is recommended that data is converted from bytestream to unicode before proceeding with processing the data. Till next time :)
