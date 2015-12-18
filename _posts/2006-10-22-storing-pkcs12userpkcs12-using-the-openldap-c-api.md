---
id: 144
title: 'Storing PKCS#12 Using the OpenLDAP C API'
author: Wyatt
excerpt: |
  Now does anyone else think that it's really stupid that the file is STORED and REQUESTED using the ";binary" transport syntax, but that you aren't allowed to use it?
layout: post
guid: http://blog.hackerforhire.org/?p=144
permalink: /2006/10/22/storing-pkcs12userpkcs12-using-the-openldap-c-api/
autometa:
  - pkcs openldap fighting certificate updated fought battles busy
categories:
  - Rants
  - Technology
---
First off, I&#8217;m sorry it&#8217;s been a while since I&#8217;ve updated. I&#8217;ve been insane busy fighting the battles that need to be fought at the house; however, I do want to document this since I can&#8217;t seem to find how to do it anywhere else on the Internet and I know that I can&#8217;t be the only other person in the world that would ever want to store a PKCS#12 certificate in OpenLDAP using C. It took a little longer because I wanted nice clean sections of code for people to look at. Kudos to the [Code Snippet [direct download]][1] plugin for making that happen, originally found at <http://blog.enargi.com/codesnippet/>. (The guys blog is down and has been for some time &#8230; I though I&#8217;d make it available to anyone else who wanted this kick-ass plugin.)

First a little background information on the &#8220;userPKCS12&#8243; object in the schema. I quote directly:  
**PKCS #12 [PKCS12] provides a format for exchange of personal identity information. When such information is stored in a directory service, the userPKCS12 attribute should be used. This attribute is to be stored and requested in binary form, as &#8216;userPKCS12;binary&#8217;. The attribute values are PFX PDUs stored as binary data. OpenLDAP note: &#8220;;binary&#8221; transfer should NOT be used as syntax is binary**

Now does anyone else think that it&#8217;s really stupid that the file is STORED and REQUESTED using the &#8220;;binary&#8221; transport syntax, but that you aren&#8217;t allowed to use it? If you do a Google on this, you&#8217;ll find a nice little mail message about someone who was trying to overcome this issue but never said how he did it &#8230; and that&#8217;s what I&#8217;m here to fix.  
<!--more-->

**Stupid! Stupid! Stupid!**  
In my search for how to pull this off, I found tons and tons of the exact information that didn&#8217;t really get you anywhere. Here are 2 myths that everyone seems to believe, but aren&#8217;t really documented as inaccurate anywhere:

**1. userPKCS12 must be Base64 encoded before you send them to LDAP**  
Err! Wrong! userPKCS12 files must be Base64 encoded IF you are using an LDIF file. Since we are using the API in C, this is a load of horse crap.

**2. userPKCS12 must be transported in UFT-8 format**  
Wrong again! If you were again using the OpenLDAP tools, yes, then you can encode the Base64/userPKCS12 (I&#8217;m not sure which, ever time I asked that I was given a bunch of crap about how I should use use the OpenLDAP tools and not write my own). The purpose is to remove the invalid binary characters that occur when you want to use something like ldap://blah.com:389.

**It doesn&#8217;t work**  
Since I love STL and their strings, that&#8217;s what I stored my userPKCS12 data in, which worked really well. I could access anything I needed, decrypt the information, pull out PEMs using OpenSSL, etc. OpenLDAP was the only bastard that wouldn&#8217;t work. Since there are a ton of great documents out there on how to use ldap\_modify\_ext_s and actually initialize the OpenLDAP library (although 2.3, all the previous functions were deprecated so you have to use all the undocumented ones that are located in the ldap.h header file &#8230; FIX YOUR DAMNED DOCS!!!), I&#8217;m going to assume you already have done that and we are merely setting up the LDAPMod*[] array that send to OpenLDAP &#8230; that&#8217;s where the problem was anyway.

Here&#8217;s the first pass that didn&#8217;t have a snowball&#8217;s chance in hell:

<pre><div class="codesnip-container" >
  <div class="c codesnip">
    <span class="kw4">string</span> strUserPKCS12 <span class="sy0">=</span> binaryPKCS12Cert<span class="sy0">;</span><br />
    LDAPMod <span class="sy0">*</span>modarray<span class="br0">&#91;</span><span class="nu0">2</span><span class="br0">&#93;</span><span class="sy0">;</span><br />
    <br />
    modarray<span class="br0">&#91;</span><span class="nu0"></span><span class="br0">&#93;</span> <span class="sy0">=</span> new LDAPMod<span class="sy0">;</span><br />
    <br />
    modarray<span class="br0">&#91;</span><span class="nu0"></span><span class="br0">&#93;</span><span class="sy0">-&gt;</span>mod_op <span class="sy0">=</span> LDAP_MOD_REPLACE <span class="sy0">|</span> LDAP_MOD_ADD<span class="sy0">;</span><br />
    modarray<span class="br0">&#91;</span><span class="nu0"></span><span class="br0">&#93;</span><span class="sy0">-&gt;</span>mod_type <span class="sy0">=</span> <span class="st0">"userPKCS12"</span><span class="sy0">;</span><br />
    modarray<span class="br0">&#91;</span><span class="nu0"></span><span class="br0">&#93;</span><span class="sy0">-&gt;</span>mod_values <span class="sy0">=</span> strdup<span class="br0">&#40;</span> <span class="br0">&#40;</span><span class="kw4">char</span><span class="sy0">*</span><span class="br0">&#41;</span> strUserPKCS12.<span class="me1">c_str</span><span class="br0">&#40;</span><span class="br0">&#41;</span> <span class="br0">&#41;</span><span class="sy0">;</span><br />
    modarray<span class="br0">&#91;</span><span class="nu0">1</span><span class="br0">&#93;</span> <span class="sy0">=</span> NULL<span class="sy0">;</span>
  </div>
</div>
</pre>

The problem with this code was that calling .c_str() *might* return the whole string, but that we are working with a very long segment of binary data (4k of data almost) so it might not really do what our orignal purpose was. If you sit back and look at it, this is really a stupid move on my part because strdup() will stop right after the first NULL it finds. It also failed because we were using the wrong LDAPMod structure value. This was the second pass to try and fix those issues:

<pre><div class="codesnip-container" >
  <div class="c codesnip">
    <span class="kw4">string</span> strUserPKCS12 <span class="sy0">=</span> binaryPKCS12Cert<span class="sy0">;</span><br />
    LDAPMod <span class="sy0">*</span>modarray<span class="br0">&#91;</span><span class="nu0">2</span><span class="br0">&#93;</span><span class="sy0">;</span><br />
    <span class="kw4">struct</span> berval <span class="sy0">*</span>pointerArray<span class="br0">&#91;</span><span class="nu0">2</span><span class="br0">&#93;</span><span class="sy0">;</span><br />
    <span class="kw4">struct</span> berval <span class="sy0">*</span>binaryData <span class="sy0">=</span> new <span class="kw4">struct</span> berval<span class="sy0">;</span><br />
    <br />
    modarray<span class="br0">&#91;</span><span class="nu0"></span><span class="br0">&#93;</span> <span class="sy0">=</span> new LDAPMod<span class="sy0">;</span><br />
    modarray<span class="br0">&#91;</span><span class="nu0"></span><span class="br0">&#93;</span><span class="sy0">-&gt;</span>mod_op <span class="sy0">=</span> LDAP_MOD_REPLACE <span class="sy0">|</span> LDAP_MOD_ADD<span class="sy0">;</span><br />
    modarray<span class="br0">&#91;</span><span class="nu0"></span><span class="br0">&#93;</span><span class="sy0">-&gt;</span>mod_type <span class="sy0">=</span> <span class="st0">"userPKCS12"</span><span class="sy0">;</span><br />
    <br />
    binaryData<span class="sy0">-&gt;</span>bv_len <span class="sy0">=</span> strUserPKCS12.<span class="me1">size</span><span class="br0">&#40;</span><span class="br0">&#41;</span><span class="sy0">;</span><br />
    binaryData<span class="sy0">-&gt;</span>bv_val <span class="sy0">=</span> <span class="br0">&#40;</span><span class="kw4">char</span> <span class="sy0">*</span><span class="br0">&#41;</span> strUserPKCS12.<span class="me1">data</span><span class="br0">&#40;</span><span class="br0">&#41;</span><span class="sy0">;</span><br />
    <br />
    pointerArray<span class="br0">&#91;</span><span class="nu0"></span><span class="br0">&#93;</span> <span class="sy0">=</span> binaryData<span class="sy0">;</span><br />
    pointerArray<span class="br0">&#91;</span><span class="nu0">1</span><span class="br0">&#93;</span> <span class="sy0">=</span> NULL<span class="sy0">;</span><br />
    <br />
    modarray<span class="br0">&#91;</span><span class="nu0"></span><span class="br0">&#93;</span><span class="sy0">-&gt;</span>mod_bvalues <span class="sy0">=</span> pointerArray<span class="sy0">;</span><br />
    modarray<span class="br0">&#91;</span><span class="nu0">1</span><span class="br0">&#93;</span> <span class="sy0">=</span> NULL<span class="sy0">;</span>
  </div>
</div>
</pre>

The problem here took me for flipping ever to find. Normally, when you specify a size and a pointer to the data segment, it should just be like &#8220;Oh sure, I can handle that.&#8221;; however, ber\_printf in the OpenLDAP code actually eats the memory in a really stupid fashion. This was tired with .c\_str() and .data() which both work with OpenSSL, yet not with OpenLDAP. The reason it took me so long to find was that it was eating the memory near the middle 3.5k mark and leaving the end intact and my debugger wasn&#8217;t showing me that. So what was the solution? I&#8217;m not going to tell you &#8230; ha, I kid &#8230; here it is.

<pre><div class="codesnip-container" >
  <div class="c codesnip">
    <span class="kw4">string</span> strUserPKCS12 <span class="sy0">=</span> binaryPKCS12Cert<span class="sy0">;</span><br />
    LDAPMod <span class="sy0">*</span>modarray<span class="br0">&#91;</span><span class="nu0">2</span><span class="br0">&#93;</span><span class="sy0">;</span><br />
    <span class="kw4">struct</span> berval <span class="sy0">*</span>pointerArray<span class="br0">&#91;</span><span class="nu0">2</span><span class="br0">&#93;</span><span class="sy0">;</span><br />
    <span class="kw4">struct</span> berval <span class="sy0">*</span>binaryData <span class="sy0">=</span> new <span class="kw4">struct</span> berval<span class="sy0">;</span><br />
    <br />
    modarray<span class="br0">&#91;</span><span class="nu0"></span><span class="br0">&#93;</span> <span class="sy0">=</span> new LDAPMod<span class="sy0">;</span><br />
    modarray<span class="br0">&#91;</span><span class="nu0"></span><span class="br0">&#93;</span><span class="sy0">-&gt;</span>mod_op <span class="sy0">=</span> LDAP_MOD_REPLACE <span class="sy0">|</span> LDAP_MOD_ADD<span class="sy0">;</span><br />
    modarray<span class="br0">&#91;</span><span class="nu0"></span><span class="br0">&#93;</span><span class="sy0">-&gt;</span>mod_type <span class="sy0">=</span> <span class="st0">"userPKCS12"</span><span class="sy0">;</span><br />
    <br />
    <span class="kw4">char</span> <span class="sy0">*</span>myUserPKCS12 <span class="sy0">=</span> <span class="br0">&#40;</span><span class="kw4">char</span> <span class="sy0">*</span><span class="br0">&#41;</span> malloc <span class="br0">&#40;</span><span class="kw4">sizeof</span><span class="br0">&#40;</span><span class="kw4">char</span><span class="br0">&#41;</span> <span class="sy0">*</span> strUserPKCS12.<span class="me1">size</span><span class="br0">&#40;</span><span class="br0">&#41;</span><span class="br0">&#41;</span><span class="sy0">;</span><br />
    memset<span class="br0">&#40;</span>myUserPKCS12<span class="sy0">,</span> <span class="nu0"></span><span class="sy0">,</span> strUserPKCS12.<span class="me1">size</span><span class="br0">&#40;</span><span class="br0">&#41;</span><span class="br0">&#41;</span><span class="sy0">;</span><br />
    memcpy<span class="br0">&#40;</span>myUserPKCS12<span class="sy0">,</span>strUserPKCS12.<span class="me1">data</span><span class="br0">&#40;</span><span class="br0">&#41;</span><span class="sy0">,</span>strUserPKCS12.<span class="me1">size</span><span class="br0">&#40;</span><span class="br0">&#41;</span><span class="br0">&#41;</span><span class="sy0">;</span><br />
    binaryData<span class="sy0">-&gt;</span>bv_len <span class="sy0">=</span> strUserPKCS12.<span class="me1">size</span><span class="br0">&#40;</span><span class="br0">&#41;</span><span class="sy0">;</span><br />
    binaryData<span class="sy0">-&gt;</span>bv_val <span class="sy0">=</span> myUserPKCS12<span class="sy0">;</span><br />
    <br />
    pointerArray<span class="br0">&#91;</span><span class="nu0"></span><span class="br0">&#93;</span> <span class="sy0">=</span> binaryData<span class="sy0">;</span><br />
    pointerArray<span class="br0">&#91;</span><span class="nu0">1</span><span class="br0">&#93;</span> <span class="sy0">=</span> NULL<span class="sy0">;</span><br />
    <br />
    modarray<span class="br0">&#91;</span><span class="nu0"></span><span class="br0">&#93;</span><span class="sy0">-&gt;</span>mod_bvalues <span class="sy0">=</span> pointerArray<span class="sy0">;</span><br />
    modarray<span class="br0">&#91;</span><span class="nu0">1</span><span class="br0">&#93;</span> <span class="sy0">=</span> NULL<span class="sy0">;</span>
  </div>
</div>
</pre>

Programmatically, this code is exactly the same as the code above with the difference that I had to malloc() my own space even though the STL string was supposed to give me a pointer to the direct data segment (which it does, OpenLDAP just clobbers it in the ber_printf() call) and I specified exactly how much data was supposed to get set into my array. Looking back I realize how this is my fault for relying on some shoddy programming tactics and that strdup() stops at null style characters; however, that still doesn&#8217;t excuse the fact that there&#8217;s a lack of a document on this massive fricken Internet that tells you how to make this magic happen. Don&#8217;t forget to free your memory so you don&#8217;t look like a crappy OpenLDAP programmer :-).

 [1]: http://hackerforhire.org/codesnippet20.zip