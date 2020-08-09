# CyberSec2020 POC

This repository is the proof of concept for ITHome CyberSec2020 Internet Security session. It will show how BGP hijacking works.  
## Prerequisties

  - VurtualBox for 3 virtual machines
  - GNS3 to simulate AS100, AS200, AS300 and AS400

## Hoew it works

AS100, AS200, AS300 and AS400 are interconnected with each other and using BGP to exchange routing information. The GOOD web site is under AS200. There is one malicious actor would like to pretend the GOOD web site and it's under AS400. Please see the following topology.
![image](https://github.com/jieliau/cybersec2020_poc/blob/master/Topology.png)

You can check it out on client virtual machine. Open the browser and surf http://www.example.com or try tracepath www.example.com. Please see below:
![image](https://github.com/jieliau/cybersec2020_poc/blob/master/GoodWebSite.png)
![image](https://github.com/jieliau/cybersec2020_poc/blob/master/Tracepath_good.png)

Then under AS400 router, please type the following command to announce 123.123.123.0/25 this more specific prefix.
```
AS400#configure terminal 
Enter configuration commands, one per line.  End with CNTL/Z.
AS400(config)#router bgp 400
AS400(config-router)#network 123.123.123.0 mask 255.255.255.128
AS400(config-router)#end
AS400#
```

Now you can check it out on client virtual machine again. Surf the same web site http://www.example.com but you will see the different content. Tracepath to www.example.com changes as well. Please see below:
![image](https://github.com/jieliau/cybersec2020_poc/blob/master/NotGoodWebSite.png)
![image](https://github.com/jieliau/cybersec2020_poc/blob/master/Tracepath_notgood.png)
