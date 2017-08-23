---
layout: history
type: Research
category: Research
tags: [PKI, attacks]
title: PKI Attacks
group: 21st Century
timeline: 2010 - today
---

Public key infrastructure (PKI) has recently seen an upsurge in its adoption. Using TLS/SSL, the “S” in HTTPS, for web services is becoming the norm with web browsers like Mozilla now <a href="//www.troyhunt.com/https-adoption-has-reached-the-tipping-point">reporting seeing more secure traffic served over HTTPS than non-secure (HTTP) traffic</a>. The SSL certificates used by HTTPS for encryption rely on PKI to provide server to client authentication. This is especially critical for e-commerce and online banking sites that regularly handle sensitive customer financial data. PKI is also being used by organizations for secure code-signing, to provide digital signatures on documents or emails or even to store certificates in smartcards as a part of two-factor authentication schemes. As the world moves further toward cloud computing, mobile and IoT (Internet of Things) devices, secure authentication is becoming more critical than ever.

<h2>Stealing Valid Digital Certificates</h2>
Certificates are used to digitally sign software updates in order to flag the software to the OS and any AntiVirus applications running on the OS as legitimate. If the certificate does not checkout via the CA either the OS or AntiVirus will block the software from running. Stealing a digital certificate from a trusted vendor and then signing malicious code with it allows malware to bypass these security controls, avoiding detection and infecting the relying party’s OS. 

Experts estimate that there are <a href="//resources.infosecinstitute.com/cybercrime-exploits-digital-certificates/">now more than 200,000 unique malware binaries in the wild that have been signed with valid digital certificates</a>. Stuxnet, a cyber weapon used to infect nuclear enrichment plants in Iran, is one of the first known exploits to use this technique. The drivers used in Stuxnet were signed with digital certificates associated with Realtek Semiconductor and JMicron Technology Corp, giving the appearance of legitimate software to targeted systems. 

Still different strains of malware have been found in the wild that are <a href="//resources.infosecinstitute.com/cybercrime-exploits-digital-certificates/">equipped to steal private keys and digital certificates from Windows certificate stores saved locally on the OS</a>. These types of attacks use the OS’s own functionality against it in order to download all private keys, root/CA certificates, and software publisher certificates stored locally on an OS. The malware can then exfil the certificates to the attacker for further use. Once a victim’s private key is acquired, the attacker can use any of a number of signing tools available to sign malicious code with the victim’s private key. 

<h2>Stealing CA Certificates</h2>
The powerful role the CA plays in the PKI model makes it a prime target for attacks. In 2011 and 2012, a series of attacks compromised various CA organizations, including DigiNotar, GlobalSign, Comodo and Digicert Malaysia. These attacks all exploited the fact that CAs are allowed to issue certificates for any application without obtaining the consent of the application owner. 

The <a href="//threatpost.com/final-report-diginotar-hack-shows-total-compromise-ca-servers-103112/77170/">attack on DigiNotar</a>, a Dutch CA owned by VASCO Data Security, Inc., is a prime example of an attack on a CA that had far reaching consequences. It enabled mass surveillance to be done on hundreds of thousands of Iranians, spurned various forms of malware signed with rogue certificates, and compromised certificates owned by government organizations. This attack was referred to as “Operation Black Tulip” and believed to have begun with the compromise in June 2011 of DigiNotar’s outward facing web server. The attacker was able to pivot through DigiNotar’s systems and corrupt all eight servers that managed DigiNotar’s CAs. With this access, attackers were able to generate and sign hundreds of rogue certificates, most notably a wildcard certificate for Google. This certificate was used with a MITM attack on Iranians, breaking HTTPS encryption used by Gmail to read private citizens’ emails.

The worst part of the DigiNotar attack was that DigiNotar detected the initial breach, but failed to report it. It wasn't until others began noticing the rogue certificates in the wild that the compromise became known, spurring browsers and other CAs to revoke all certificates that had been signed by DigiNotar. Within a month of the breach, the company declared bankruptcy.

<h2>Man-In-The-Middle (MITM) Attacks</h2>
There have been several instances where certificates have been abused to intercept TLS/SSL communications. These aren’t always situations like DigiNotar where an attacker is specifically stealing certificates to intercept traffic. There are other cases too, like that of <a href="//www.zdnet.com/article/nokia-hijacks-mobile-browser-traffic-decrypts-https-data/">Nokia</a>, where companies set up their systems to pass secure communications through their servers, providing them the ability to decrypt messages for data collection before passing them along to their destination. While not always intended to be malicious, these types of abuses of power in the “chain of trust” are hard to detect and exposes sensitive data to unauthorized systems.

<h2>Weak RA and CA Processes</h2>
When CAs issue weak or improper certificates, attackers are given yet more opportunities to abuse a certificate to sign malware or spoof legitimate sites. Several CAs, such as DigiCert, have failed to authenticate requestors properly and <a href="//zeltser.com/how-digital-certificates-are-used-and-misused/">issued certificates to companies that do not exist</a>. These certificates were later discovered to have been used to sign malware. Still other CAs have been <a href="//zeltser.com/how-digital-certificates-are-used-and-misused/">found to use weak encryption methods</a> that enable a signer's or CA's private key to be extrapolated from the public key. Having the private key then allowed them to spoof the signer's certificate in spear phishing attacks.

To make matters worse, if a certificate is discovered to be fraudulent or compromised the process of updating the CRLs is <a href="//news.netcraft.com/archives/2013/05/13/how-certificate-revocation-doesnt-work-in-practice.html">at best slow and at worst broken</a>. Updates to CRLs are pushed out to clients at intervals, meaning it could be hours or days before a client receives the updated list. For some the situation is far worse as many web browsers have been shown to fail to check the CRL entirely, allowing revoked certificates to continue to be used for weeks if not months.

<h2>Hiding Malicious Traffic</h2>
The growth in the usage of SSL/TLS has increased for both legitimate and malicious activities alike. Attackers now use these tools to aid in the distribution and control their malicious content. In the past six months alone, <a href="//www.csoonline.com/article/3212965/cyber-attacks-espionage/why-ssl-tls-attacks-are-on-the-rise.html#tk.csoendnote">a security researcher at Zscaler has reported that attacks using SSL/TLS have more than doubled</a>. Free CAs like Let’s Encrypt now issue certificates with little to no validation. While this has greatly reduced the barrier to entry to HTTPS for a lot of smaller websites and users, it opens the door for HTTPS to be weaponized. Now malicious sites appear “secure” with the green lock appearing in a user’s browser, giving users a false sense of security that the website is legitimate. 

To conflate the issue, any interactions with this site are now entirely encrypted. Meaning many security tools which scan traffic for indicators of malicious activity will be unable to detect if anything malicious is passed to or from the system. In this case, no spoofing on the part of the attacker is required, the certificate was issued correctly by a CA. To be fair, many CAs make an effort to revoke certificates that are known to be associated with malicious activity once reported.

<h2>Exploiting the End User’s Trust Store</h2>
Similar to how malware can collect certificates from a user’s OS, attackers can also install a fake root CA certificate onto a compromised system. This way that any site or software using this fake root CA will be overlooked by any security tools running on the system. <a href="//zeltser.com/how-digital-certificates-are-used-and-misused/">Spyware has used this technique so it can act as a local proxy on the system for all SSL/TLS traffic</a> in order to break encryption and collect data on the user. Other variants have used this attack to quiet security warnings that would normally pop up when malware infected the user’s system.

<h2>List of Rogue Certificates</h2>
As a side note, this abuse of certificates has grown so bad that security researchers have made a concerted effort to track these malicious activities. Sites like <a href="//sslbl.abuse.ch/">SSL Blacklist</a> were created to try and keep a running list of all fraudulent certificates that have been found connected to malicious activities. This website currently contains over 130,000 blacklisted certificates. 