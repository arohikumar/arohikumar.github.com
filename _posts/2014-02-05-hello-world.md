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
 
Example coming soon :) Hope you enjoyed that. 
