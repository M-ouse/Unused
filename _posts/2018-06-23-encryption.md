---
layout: post
title:  "RC4 Encryption & Decryption"
image: ''
date:   2018-06-22
tags:
- RC4
description: 'Basic'
categories:
- Encryption
---

## The example of Python is as follows:

{% highlight Python %}
# coding=utf-8

class RC4:

    def __init__(self,public_key = None):
        if not public_key:
            public_key = 'none_public_key'
        self.public_key = public_key
        self.index_i = 0;
        self.index_j = 0;
        self._init_box()
 
    def _init_box(self):
        """
        Initialization substitution box
        """

        self.Box = range(256)
        key_length = len(self.public_key)
        j = 0
        for i in range(256):
            index = ord(self.public_key[(i % key_length)])
            j = (j + self.Box[i] + index ) % 256
            self.Box[i],self.Box[j] = self.Box[j],self.Box[i]

    def do_crypt(self,string):
        """
        Encryption/Decryption
        string : the string which will be encrypted/decrypted
        """

        out = []
        for s in string:
            self.index_i = (self.index_i + 1) % 256
            self.index_j = (self.index_j + self.Box[self.index_i]) % 256
            self.Box[self.index_i], self.Box[self.index_j] = self.Box[self.index_j],  self.Box[self.index_i]

            r = (self.Box[self.index_i] + self.Box[self.index_j]) % 256
            R = self.Box[r] # generating pseudorandom number
            out.append(chr(ord(s) ^ R))

        return ''.join(out)
{% endhighlight %}

## The example of C++ is as follows:

### rc4.h
{% highlight C++ %}
class RC4
{

public:
    RC4();
    
    void rc4_init(unsigned char *key, unsigned long Len);
    
    // Encrypt/Decrypt
    void do_crypt(unsigned char *Data, unsigned long Len);
    
private:
   
    int m_box[256]; // S box
    int m_index_i;
    int m_index_j;
};
{% endhighlight %}

### rc4.cpp
{% highlight C++ %}
RC4::RC4()
{
    m_index_i = 0;
    m_index_j = 0;
}

// init algorithm
void RC4::rc4_init(unsigned char *key, unsigned long Len)
{
    if (key == NULL || Len == 0)
    {
        printf("rc4 key or len is 0, return! ");
        return ;
    }
    
    // for loop 0 to 255 non repeating elements in the S box
    for (int i = 0; i < 256 ; i++) {
        m_box[i] = i;
    }
    
    // for loop to disrupt the S box based on the key
    int j = 0;
    unsigned char tmp;
    for (int i = 0; i < 256; i++)
    {
        j = ( j + m_box[i] + key[i % Len] ) % 256;
        
        tmp = m_box[i];
        m_box[i] = m_box[j]; //Swap m_box[i] and m_box[j]
        m_box[j] = tmp;
    }
}
    
void RC4::do_crypt(unsigned char *Data, unsigned long Len)
{
    /*
    Each byte is received, and the while loop is carried out. An algorithm ((a), (b)) is used to locate an
    element in the S box and get k with the input byte XOR. The S box is also changed in the loop ((c)).If
    the input is plaintext, the output is ciphertext; if the ciphertext is input, the output is plaintext.
    */
    unsigned char tmp;
    for(unsigned long k = 0 ; k < Len ; k++)
    {
        m_index_i = (m_index_i + 1) % 256;    // a
        m_index_j = (m_index_j + m_box[m_index_i] ) % 256; // b
        
        tmp = m_box[m_index_i];
        m_box[m_index_i] = m_box[m_index_j]; //Swap m_box[x] and m_box[y]
        m_box[m_index_j] = tmp;
        
        // Generating pseudorandom number
        int r = ( m_box[m_index_i] + m_box[m_index_j] ) % 256;
        Data[k] ^= m_box[r];
    }
    
}
{% endhighlight %}
C++ link : [https://www.jianshu.com/p/fcfdcc3ff9d5](https://www.jianshu.com/p/fcfdcc3ff9d5)