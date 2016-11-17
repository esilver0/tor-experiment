# Anonymity of Network Traffic Using Tor

## I. Background
Today we live in a world where the Internet is accessible from almost anything that we have in our possession. However as Internet continues to become more expansive and accessible, the attacks on people using the Internet by spying on and stealing their information also increases. Nowadays we never know who may be in between you and your friend when sending text messages. How is this problem being solved in today's world? Well if there was no possible solution, I would not be writing this today. Let us take a deep dive into this solution, known as Tor.

### Overview of Tor
Tor, which stands for The Onion Router, is a software that protects you from people on the Internet who are trying to spy on you. Tor has a network of routers that keeps your identity hidden by moving your traffic across its network before your traffic is sent to its destination. In this way, when your traffic reaches the final destination, someone spying on you would not know who actually sent that specific data packet. Even the site which is your destination would not know from where the traffic is coming from. In this way, people who use Tor are able to browse the Internet anonymously without ever revealing their location.

Why was Tor built in the first place? Let us first take look back at the history of Tor when it was first created. Tor was originally developed by the US military for the purpose of providing some kind of cloaking mechanism of the identity of government personnel when they worked online[1]. Mainly funded by the Office of Naval Research and DARPA (Defense Advanced Research Projects Agency), the main goal of creating Tor was to provide anonymity for military and intelligence operations that require the use of public communication infrastructure and/or databases[1]. This was their primary objective, and perhaps the only one. The developers of Tor knew that their software would be able to be used by other people for other reasons beyond their control. People would be able to use Tor to commit crimes all while cloaking their tracks. Even while knowing this, the development of Tor continued and was marketed for everyone to use because the primary objective remained as the top and only priority. Everything else was secondary.

In fact, other than those who would use Tor for cloaking criminal activity, the US Navy needed other people other themselves to use Tor. Using a cloaking software exclusively by the US Navy would conversly decloak the people, because an attacker watching the Tor network would know that anything that goes in or out of the network would be by the US Navy. The US Navy required as diverse of a community of people as possible to use Tor in order to hide themselves behind everyone. This was an essential part in fulfilling their primary objective of cloaking the identity of government and intelligence personnel, which was why Tor became a consumer product that everyone would be able to use. Everything was a balance of priority: Tor would not be the perfect to solution for everything, but it would at least be a solution for their primary objective. The crime that comes out of releasing Tor to the public would need to be dealt with at a later time. 

![](http://geography.oii.ox.ac.uk/wp-content/uploads/2014/06/Tor_Hexagons.png)

*Data Source: Internet Geographies at the Oxford Internet Institute*

We can see from the above image that the number of Tor users other than those of the US Navy in fact did increase immensely by placing it on the market. Who are these people that are using Tor? A main group of users of Tor are journalists and activists that live in countries that place restrictions on the Internet. For example many journalists in China use Tor to get past China's national firewall in order to write about events occurring locally around them, in order to create commotion regarding both social and political reform[2]. Other groups of people that want to raise their voice to the public without revealing their identities include activists, whistleblowers, bloggers, and high and low profile people. Tor is also used by law enforcement officers for surveillance of sites that may potentially be used for illegal criminal activity or illegal gambling. Above all these groups of people however, a large group of users of Tor are people who simply with to evade surveillance and protect their privacy when browsing the Internet.


### An Overview of Tor's Security
How does Tor actually work? Tor is a software that can run in conjunction with HTTPS, which further increases its security capabilities. HTTPS (Hypertext Transfer Protocol over TLS) is a secure communication protocol used widely in the Internet, which provides authentication of accessed websites and provides privacy of the data that is exchanged between the client, web server, and the website[3]. Encryption of data also occurs, which protects the user from attackers that spy on the network to steal the user's information. Let us take a look at the following example of a simple network to further see the capabilities of Tor and HTTPS.
![](https://github.com/tfukui95/tor-experiment/blob/master/~Tor~HTTPS.PNG)  
*Data Source: Electronic Frontier Foundation (EFF): Tor and HTTPS*  
(Question for Fraida: Am i able to not just copy the picture but the simulation with the buttons?)

The above network shows a number of users/nodes with different roles: user, hacker, NSA, ISP, and others who have data sharing either with the ISP or the site that the user is accessing. The source is the user who is on the laptop, and the destination is the black box named Site.com. The yellow box next to each node represents what information about the network the node can see. We can see that in the above network, every node can see all the information that is being exchanged between the user and the website. This includes the site that the user is accessing, the username and password used to access the site, the actual payload/data that is being exchanged, and the location of the user. This specific scenario is when neither Tor nor HTTPS is being used by the user to access the website. For a hacker, such a case is paradise because they can see everything that you send, and can even steal your username and password information and pretend that they are you and do malicious activities. Users who have data sharing with an ISP are usually law enforcement people who have the rights to access this kind of information. In this case where neither Tor nor HTTPS is used, they can also see all of your information. Next we have the NSA (National Security Agency) which either spies on the network or has secret access to the network through the ISPs. The NSA's aim is primarily to deanonymize users who are using Tor as a method to commit crimes without leaving any tracks. The NSA takes control of web servers by placing their own secret servers to impersonate a specific illegal site and to send malware to the users accessing that site. When neither Tor nor HTTPS is used, the NSA can easily view and access your information. Lastly, the user clearly knows all of the information about itself, and the accessed website also does as well. 

Now let us examine what happens when we use HTTPS to access a website:
![](https://github.com/tfukui95/tor-experiment/blob/master/~TorHTTPS.PNG)   
*Data Source: Electronic Frontier Foundation (EFF): Tor and HTTPS*  
We can clearly see that the user, the website, and those that have data sharing with the website still see the all the information. This is expected because the user and the site are the ends of the network, and HTTPS is responsible for encrypting the information that travels between both ends. Due to this encryption, the rest of the network can longer see the username and password of the user, and the data that is being sent to the site. Even with data sharing on the ISP, these nodes cannot decrypt the information. The data sharing must be the site itself to have access to the unencrypted information about the user and the data sent.  

Now let us examine what happens when we only use Tor to access a website:
![](https://github.com/tfukui95/tor-experiment/blob/master/Tor~HTTPS.PNG)   
*Data Source: Electronic Frontier Foundation (EFF): Tor and HTTPS*  
We now observe that in between the two NSA nodes, there are now three new nodes, which represent three tor relays. The hacker, the nodes sharing data with the first ISP, and the first NSA node can only see the location of the user sending traffic. They do not know the username information, the data the user is sending, nor the site that the user is accessing. Why is this the case even when the user is not using HTTPS? This is because Tor also encrypts the information in which the tor relays can only decrypt. This encryption process begins with the user running the Tor software's special proxy called the onion proxy (OP). The OP then accesses a special kind of onion router called the directory server, which is a certain reliable node that provides directories that contain known routers, including their location and current state. Using the directory the OP determines which routers are going to be used, negotiates the encryption keys for each router, and encrypts the packet accordingly. Therefore a user's traffic is encrypted at the user stage by the onion proxy. The reason why the nodes before the first tor relay do not even know which site the user is accessing is because the user's traffic destination is initially the first tor relay in the circuit. Each tor relay in the tor network only knows the certain amount of information that they can decrypt, which is why it becomes harder for hackers and other people spying on one's traffic to figure out who is communicating with who. The specific processes that occur in the Tor process will be explained in much greater detail in the next section, **Diving Deeper into the Tor Process**. The last tor relay knows the username information, the data being sent, and the site to access because it is the exit relay's job to send the data to the site. At this point the traffic exits the tor network and is no longer encrypted. Mostly everything can be seen by the nodes that are eavesdropping on the network, except for one important piece of information: the user location. After having been bounced around the tor network, the traffic no longer contains the original user's location, which makes it difficult to match which user is accessing the site. However since the user information and data can still be seen, this information can be stolen which is a weakness of using Tor.

We resolve the problem that nodes eavesdropping the second ISP have access to user information by using Tor in conjunction with HTTPS.  
![](https://github.com/tfukui95/tor-experiment/blob/master/TorHTTPS.PNG)  
*Data Source: Electronic Frontier Foundation (EFF): Tor and HTTPS*  
The information that the nodes before the entry Tor node can see is still the same, which is very limited. The biggest change that we can see is that the nodes eavesdropping on the second ISP which is after the Tor network can no longer see the username and password, along with the data that is being sent. This includes the exit relay as well. This is the case because the original traffic being sent from the user is now encrypted with both Tor and HTTPS. When the traffic reaches the exit relay and leaves the Tor network, it is no longer encrypted by Tor, but is still encrypted by HTTPS from beginning to end. However we observe that the exit relay still knows the site to access because it still has to perform its job to deliver the HTTPS encrypted traffic to the site that it is being told to access. Lastly we can see how the website and the nodes sharing data with the site clearly know the username information and data because the traffic's HTTPS encryption is decrypted at the destination. However the location of the original user is still unknown, maintaining privacy and security. Using Tor on top of HTTPS provides security immeasurably greater than using neither or even one or the other. From this example the capabilities of Tor in protecting and cloaking a user from hackers and eavesdroppers were clearly seen.


### Diving Deeper into the Tor Process
Now that we know what Tor is and the benefits of using Tor to protect your privacy and security, let us examine what goes on behind the scenes of the Tor network. The Tor network consists of onion routers (OR), or nodes that a Tor user's traffic passes through before reaching its destination. There are three main kinds of ORs: entry node, relay node, and exit node. The entry node is where the user's traffic first enters the Tor network. The exit node is conversely where the traffic exits the Tor network. Any nodes in between are relay nodes that simply pass the traffic from one node to the next. The specific functions of each OR will be explained later in the section. Among these ORs there is a special kind of OR called the directory authority (DA), which is a certain more trusted, reliable OR that contains a list of known ORs in the network, including their location and current state. 

The Tor network is constantly changing, and there needs to be some kind of mechanism so that the DAs in the Tor network are constantly aware of these changes that occur. This is where keys come into play. A DA has three kinds of keys: an authority identity key, an authority signing key, and an authority certificate[4]. In order to keep information about the DA up to date, it must sign directory information about itself periodically. This is done by the authority signing key. The authority signing key is not a permanent key, and is replaced around every 3-12 months. In order to authenticate the signing key, a DA has an authority certificate. This certificate must also be authenticated, which is done by the DA's authority identity key. This identity key is a long term key which as the name explains, identifies that the DA truly is a DA. 

Now that we know the mechanism in which a DA's status is constantly updated, let us take a dive into a similar process for the rest of the ORs in the Tor network. An OR has four kinds of keys: a secret id key, a secret onion key, a secret onion key ntor, and a fingerprint. The secret id key is similar to the authority identity key, and is used to sign the router's descriptor, TLS certificates, and to sign directories. A router descriptor contains the specifications of that router, including its keys, location, bandwidth, exit policy, and other minor details[5]. The reason to sign directories comes from the necessity to constantly keep the directories updated about all of the ORs, so that the directory authority can provide up-to-date information to the OP and client. The secret onion key is a key that is used when establishing a tor circuit to pass traffic along its network. These keys are not permanent unlike the identity key, and are changed every so often in order to prevent any form of compromise. The onion key also creates short-lived keys used to access TLS connections to communicate with one another and the user[5]. The secret onion key ntor is a short-term key used specifically for the opening of a tor circuit, when a three-way handshake is required. The fingerprint key, as the name suggests is a fingerprint of the identity key, used so that the identity key's location and security is preserved.

ORs pass traffic along the Tor network in fixed-size cells/packets of 512 bytes. Each cell is encrypted in many levels, where these levels are decrypted by a key at each OR until it reaches the exit node where it is then sent to the website. There are two main types of cells: control cells and relay cells. 

![](https://github.com/tfukui95/tor-experiment/blob/master/.PNG)   
*Data Source: https://svn.torproject.org*   
The above shows the structure of a cell, where the top is the control cell structure and the bottom is the relay cell structure. The control cell contains three parts: CircID, CMD, and DATA. CircID is the circuit identifier which specifies which circuit is being referred to. CMD is the command to be done, and DATA is the payload, which contains specific instructions for the command. 

## References
[0] "Somehting importatn", somebody. [link to page](http://somepage.txt)  
  [1] [https://pando.com/2014/07/16/tor-spooks/]  
  [2] [https://www.torproject.org/about/torusers.html.en]  
  [3] [https://www.instantssl.com/ssl-certificate-products/https.html]  
  [4] [http://liufengyun.chaos-lab.com/prog/2015/01/09/private-tor-network.html]
  [5] [https://svn.torproject.org/svn/projects/design-paper/tor-design.pdf]
  
