---
title: Why VideoCoin is Doomed to Fail
date: "2019-08-14T22:12:03.284Z"
---
### What is VideoCoin? ###

VideoCoin is a proposed decentralized application that provides access to cloud video infrastructure by connecting miners who perform video encoding, storage, and delivery services to clients who want to purchase those services and view videos. Miners earn VideoCoin by correctly completing video infrastructure tasks, and clients pay with VideoCoin.

### Why does VideoCoin matter? ###

Video currently constitutes 57% of all Internet traffic, and is projected to grow to 82% in 2021. In order to stream videos to customers, services such as Netflix and YouTube perform cloud infrastructure tasks, including encoding, storage, and delivery  (via content delivery networks/CDN). 

By giving miners an opportunity to perform video infrastructure tasks that companies such as Amazon, Google, and IBM currently perform, VideoCoin has the potential to provide a better-than-free model for miners. VideoCoin can also provide a competitive service for clients given a large, geographically well distributed, and reliable network of miners that can quickly encode, store, and deliver videos to those clients. 

#### My thoughts on VideoCoin ####

Initially, the high growth potential of the cloud video infrastructure market excited me, and I was compelled to find out more about how VideoCoin can fit in this market landscape. But as I delved deeper into the project, I found that VideoCoin's barriers to success, namely its need for a large network size and its low potential miner rewards, are greater than VideoCoin's strengths. First, we will discuss VideoCoin's plan to perform cloud video infrastructure tasks, and analyze its strengths and weaknesses. 

### What constitutes cloud video infrastructure and how does VideoCoin offer these services? ###

Cloud video infrastructure is composed of three main processes that allow videos to be viewed on any device almost anywhere. First, videos are encoded to fit different colorspaces, resolutions, and codecs. Videos are then stored in storage networks that can be accessed when clients want to view videos. Finally, videos are cached in places geographically close to where the client is viewing the video. VideoCoin proposed decentralized solutions to each cloud video infrastructure task, which we will analyze for strengths and weaknesses. 

#### Encoding ####

VideoCoin plans to encode videos by using an open source framework called ffmpeg. Although ffmpeg will be used in a secure container, security issues may arise because ffmpeg works with a lot of unprotected data. This can be mitigated if VideoCoin hires ffmpeg contributors to fix major security issues.

Since the CPU requirements for encoding videos are high, VideoCoin will split each video into many segments and process them simutaneously using different miners. After encoding, the segments are stitched together.  

One strength VideoCoin has is its method to prove that an encoding job was completed correctly. To confirm and verify that a miner did not cheat, a verifier node chosen from a verifier pool pulls a random segment of the video and performs the same transcode operation that the miner did; if the two sequences of frames are the same, the miner successfully completed the job. If they are not the same, the miner partially encoded or did not encode the video. VideoCoin then burns that miner's staked tokens. The verifier pool (other nodes trying to become the verifier node) can determine whether or not the verifier node's block of approvals is valid; if malicious acts are detected, the verifier node's staked tokens are burned. This cheating-prevention process for both miners and verifier nodes makes it a financial strain to keep cheating on the network and encourages good behavior. 

#### Storage ####

VideoCoin plans to use a distributed file storage system similar to Hadoop Distributed File Storage (HDFS), allowing storage miners to use their computer disk space for storing video segments. These segments will then be stitched together before being sent to the client. Since VideoCoin is using a system similar to HDFS, we can analyze HDFS to see if VideoCoin's distributed file storage system will work well. 

##### HDFS #####

HDFS is a distributed storage system that stores files in specific block sizes. For example, since HDFS has a block size of 128MB, a 256MB file will be split into two blocks. However, if a file is smaller than 128MB, the file will still take up one block (128MB) in a higher abstraction level even though it uses less physical system storage space.

HDFS also works better with larger files. When a client wants to merge or stitch files together, a map task function is called that processes one block at a time. If there are many small files that each take up one block, many more map tasks need to be called and more physical system storage space will be wasted. However, large file sizes work well with HDFS because you need fewer map tasks due to the high block size (128MB) and you have less wasted storage space. 

##### VideoCoin's Distributed File Storage System #####

In VideoCoin, each video is split into many smaller segments that miners encode simultaneously. Since VideoCoin uses an HDFS-like system, we can say that each video segment takes up one block. An HDFS-like system will work well for VideoCoin because videos have large file sizes (ex. 1 min of 720p 30fps HD with a data rate of 5MBPS is 300MB), which will be a huge benefit for rapidly stitching encoded video segments together into a single video for clients and ensuring that storage miners don't run out of storage space. 

#### Content Delivery Networks (CDN) ####

VideoCoin plans to stream videos to clients using miners that act as proxy servers, which are layers between the client and the Internet created to provide increased  network performance. 

One major flaw with this CDN plan is that proxies can be vulnerable to attacks from external actors and the actual proxies. Miners who choose to give Internet bandwidth to VideoCoin may be especially vulnerable to attacks because we cannot assume those miners will take security measures and VideoCoin does not have a plan for bolstering security. Malicious external agents can access networks by hacking into proxy servers and can affect the VideoCoin network by changing streams or shutting them down. Miners who create malicious proxy servers can also steal data such as usernames and passwords. If these agents attack the VideoCoin network, clients will flock to other services, making the network dramatically lose value. 

### What are the primary barriers to success? ###

VideoCoin's primary barriers to success are its low potential miner rewards and its
need for a large network size. When miners win a job, they commit to completing that job in exchange for a miner reward. After analyzing similar cloud video infrastructure products from Amazon Web Services and IBM, I calculated that for a 300MB video (1 min of 720p 30fps HD with a data rate of 5MBPS), total encoding, storage, and CDN costs are between $0.035085-$0.036085. 

##### AWS and IBM HDFS Listed Costs for Cloud Video Infrastructure: #####

| Infrastructure Task | Cost |
| --- | --- |
| Encoding | $0.034 per minute HD video 720p or above |
| Storage | $1000 - $2000 per TB |
| CDN | $0.085 per GB |

##### Costs of a 300MB 720p HD one minute video using competitor services: #####

| Infrastructure Task | Cost |
| :------------------- | :---------------------------- |
| Encoding | $0.034 per minute HD video 720p or above |
| Storage | $0.001 - $0.002 per MB |
| CDN | $0.00085 per MB |

##### Total: $0.035085 - $0.036085 #####

Clients who want to use VideoCoin either will demand a similar price or a significantly better experience. Since VideoCoin's CDN has security risks, a significantly better experience than AWS and IBM HDFS is unlikely at this point. If we assume that VideoCoin must charge a similar price to remain competitive, miners who choose to perform all three jobs can collectively only make about $0.03 per job. Since the time it takes to complete these tasks depends on the specifications of the miner's computer, predicting miner rewards per minute or per hour is difficult. What we do know is that VideoCoin will have to persuade individual people to try out an unproven network for the prospect of winning $0.03 per job and without knowing their own projected rewards per unit time. 

Now, I will show that VideoCoin will fail whether or not their rewards attract miners. If we assume that the miner rewards are too low for miners, the miners will not join the network. Without enough miners, the network size will be too low to provide a low latency service for all users. This is because proxy servers and storage networks will most likely not be geographically close to many users. Clients will switch to services such as Hadoop or Amazon that have more stable service failure guarantees. If we assume that miner rewards are good enough for miners, miners will choose to join VideoCoin's network. However, the price for encoding is significantly higher than storage and CDN. Miners will choose to perform only encoding tasks, which will create problems when clients want to stream videos. VideoCoin provided no mechanism for adjusting the rewards of individual tasks, so we do not know whether or not rewards will be adjusted due to demand and how exactly rewards will be calculated. Clients will switch to services that have more stable price guarantees and low risk of problems when accessing or streaming videos. 

