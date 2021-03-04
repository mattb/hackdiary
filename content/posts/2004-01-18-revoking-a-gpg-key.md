---
title: Revoking a GPG key
author: Matt Biddulph
type: post
date: 2004-01-18T17:05:52+00:00
url: /2004/01/18/revoking-a-gpg-key/
categories:
  - misc

---
A couple of months ago, I lost my [lovely laptop][1] in a burglary. This weekend, [Edd][2] reminded me that my GPG private key was on the machine, so I performed the necessary rituals to revoke it. I found the documentation on this a little sparse, so here are the steps I took.

<!--more-->

<pre class="codeblock">$ gpg --gen-revoke 6382285E</pre>

6382285E is the ID for [my key][3]. You&#8217;re asked if you want to provide a reason for the revocation (key comprised, superseded or no longer used) and an optional free-text description. After supplying your passphrase, an ascii-armoured key block is printed out. Paste this text into a file. In my case, it looked like this:

<pre class="codeblock">-----BEGIN PGP PUBLIC KEY BLOCK-----
Version: GnuPG v1.2.4 (GNU/Linux)
Comment: A revocation certificate should follow

iGwEIBECACwFAkAKbmwlHQJLZXkgd2FzIG9uIGEgbGFwdG9wIHRoYXQgd2FzIHN0
b2xlbgAKCRBQw2pwY4IoXlv4AJ0XgWhSuSwv2jpd2ifFA5IXyijnEACfXfn/qtfq
KyMdShD0odXAliKD43w=
=mRL+
-----END PGP PUBLIC KEY BLOCK-----</pre>

This step could be performed when you first generate your key, and the results stashed in a safe place for later use if you lose it. In my case, I&#8217;d kept a backup copy of the original keypair, so I was able to generate a revocation after the event.

<pre class="codeblock">$ gpg --import my_revocation.txt</pre>

Issuing this command imports the revocation into your keyring, revoking your key.

<pre class="codeblock">$ gpg --keyserver pgp.mit.edu --send-keys 6382285E</pre>

This send the revoked key to the public keyserver at pgp.mit.edu. If it succeeds, you&#8217;ll get the message &#8216;``gpg: success sending to `pgp.mit.edu' (status=200)``&#8216;. If you check your key&#8217;s verbose index page on pgp.mit.edu, you&#8217;ll see `*** KEY REVOKED ***` on the first line of the details.

For the record, my new key has the ID [097891DA][4].

_Update:_ I just found the official word on how to do this. It&#8217;s in [question 4.17 of the gpg faq][5].

 [1]: https://www.hackdiary.com/archives/000025.html
 [2]: https://usefulinc.com/edd/blog
 [3]: https://pgp.mit.edu:11371/pks/lookup?search=0x6382285E&op=vindex
 [4]: https://pgp.mit.edu:11371/pks/lookup?op=get&search=0x097891DA
 [5]: https://www.gnupg.org/documentation/faqs.en.html#q4.17