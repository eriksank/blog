#Protecting sensitive user information

There is nothing as embarrassing as having user information stolen, revealed, and abused. The user will rightly blame the service provider for not having protected his private data sufficiently. Existing practices to protect sensitive data have become insufficient. I think that we should stat making use of the fact that it is very hard or impossible to locate hidden tor servers and therefore to attack them, in order to protect sensitive user information.

Obviously, the first line of defense is to avoid collecting any more personal data from the user than strictly necessary. Every piece of information must be assessed against a real and unavoidable need to know. Otherwise, the system should reasonably try to prevent the user from supplying such information in the first place.

##The front-end server can be attacked

When setting up a site on the internet, the users will have to be able to find it. Therefore, the DNS system will have to reveal the IP address of such public front-end server. This is a problem. The server may be storing usernames, user identities, passwords, email addresses, transactions, or even worse, crypto-currency wallets. All of this information can be abused by the attacker. Therefore, this information should not be stored in a publicly-accessible location.

##Hide sensitive user information in a hidden tor server

The location of a server on the tor network is hidden. Instead of storing sensitive data on the front-end server, it is possible to store it on a hidden tor server. Even if the front end server is itself already a hidden tor server, the most sensitive information should still be separated out and stored in another hidden tor server, whose location is also hidden from the first hidden tor server.

##Prevent fishing for data

The front end server should not have a list or overview of what sensitive data is available. It is also important that the hidden tor server never answers wholesale inquiries. The tor server should only answer the very limited number of questions to which the front end server really needs answers. Example of a query protocol:

* authenticate(userAddress,pwd) => ok
* findUserByUserAddress(userAddress) => ok
* findUsers() => not ok, too broad

A user address can be an email address or a [bitmessage address](https://bitmessage.org/wiki/Main_Page) depending on the preferences of the user. Bitmessage addresses are preferred, but not all users are already familiar with them.

The hidden server should not answer on any other ports than on the designated one. The front end server may not store identifiable usernames, user addresses, or userids in any of its tables or files. It should also not be possible to guess a userid. Therefore, a userid should be a cryptographical address, similar to a bitcoin or bitmessage address. Example:

	$ bitcoind getnewaddress test
	1M6EuRKbKq2fsip4WTCYxe4qbqtpKub8fU

Without knowledge of the internal user address, it will therefore not be able to discover what real identity is associated with it, just by making educated guesses. The hidden tor server should also not answer any questions outside the few questions specifically allowed by the query protocol. The query protocol's language itself must be strictly defined by formal and [very restrictive grammar](http://en.wikipedia.org/wiki/GNU_bison). It should not be parsed manually on the side of the hidden tor server.

##Database design

It is also important to make sure that the database and files on the front end server are effectively unusable and meaningless, without access to the hidden tor server. All fields and files that do not need to be searched nor indexed by the system in its normal operation should therefore be encrypted, using an [encryption key](http://thinkdiff.net/mysql/encrypt-mysql-data-using-aes-techniques) associated and specifically generated for the user account.

For example, the content of messages, product names, comments, and so on, must not be stored in plaintext. As the data for each user is encrypted with another key, it should not be possible to wholesale decrypt the database. Only successful authentication by the user may trigger the release of the key from the hidden tor server to the front-end server in order to encrypt and decrypt his data. If the user does not log in, the front end server will have no way of reading his data.

##Two onion addresses

The beauty of the tor protocol is that even if an attacker compromises the front end server, he will still not gain enough information to also attack the hidden server, simply, because the front end server itself does not know where the hidden tor server is located. The attack will be strictly limited to using the query protocol. However, without knowing a user address, it will not be possible to obtain any relevant answer from the hidden tor server. Therefore, the attacker subjecting the front-end server to covert surveillance will only be able to attack the small subset of users who are effectively logged in, until detection takes place.

The hidden tor server should use two different onion addresses. On one onion address, the server only answers queries. On the other onion address the administrator can access the hidden server to manage it.

I have generated the following example addresses with https://github.com/katmagic/Shallot:

	./shallot ^hello
	Found matching domain after 24749399 tries: helloxgdwxjlfhiy.onion

	./shallot ^admin
	Found matching domain after 93440407 tries: adminval3urtcd6x.onion

Both onion addresses are tied to the same hidden tor server. Only the front end server knows the `helloxgdwxjlfhiy.onion` address. Nobody else should. The privacy of this address can still be compromised by an attacker. However, the damage will be limited to the email- and bitmessage addresses that the attacker is able to guess. It is exceedingly hard to guess or enumerate the bitmessage address space.

##Examining the knowledge of the front end server

It is very possible to inadvertently reveal too much information in the database and the files stored in the front end server. Even if the payload information is encrypted, it may still be possible for an attacker to discover much more information than desired, just by examining the relationship between the data.

Therefore, it may be required to purge the front end server from data related to completed transactions and that can be archived:

* archiveDbRow(table,id,jsondata)
* archiveFile(filePath,dataBlob)

Therefore, there should not be any protocol command for the front end server to retrieve archived data from the hidden tor server. The front end server should [shred](http://www.cyberciti.biz/tips/linux-how-to-delete-file-securely.html) any files archived in the hidden tor server.

##The admin address

There is never a need for the front end server to know the `adminval3urtcd6x.onion` address. The admin should actually never disclose this address to anybody. This address is really as sensitive as the admin login itself. The admin should avoid logging in to the hidden server using its public IP address. An attacker may observe that the admin makes connections to that particular IP address and conclude that it is the hidden server that he wants to attack. 

##Automatically shutting down the hidden tor service

Unless the admin re-activates the hidden tor service on a periodic basis, say, every week or every month, the front end address `helloxgdwxjlfhiy.onion` should automatically shut down and become inaccessible. The system should also automatically start sending bitmessages (preferably not email messages!) to the users that the front end may be compromised and request the users not to log in. 

##Automatically notifying users that the front-end server has been compromised

A compromised front-end server may be used by the attacker for surveillance and for recording user data and transactions. The longer the surveillance lasts, the more damage the attacker can inflict. If possible at all, the front-end server itself should also be a hidden tor server. However, not all users are willing to install the tor client required to access the tor network. Furthermore, protecting users and their financial information by using the tor network is unfortunately not yet common practice, while such additional levels of security may seriously inconvenience the user. 

