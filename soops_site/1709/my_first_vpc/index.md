My first VPC, my little buddy
=============================

While studying for the last of the associate certifications, I realized that if I was ever asked during an interview to log in and show what I have done, my AWS accounts would look like a kid’s toy chest, much played with but never organized. Creating a Virtual Private Cloud (VPC) is such a core skill, and it was finally time to rein in my personal account. I’ll tackle work on Monday.

I’ve used the VPC wizard before, but today was kind of a test for me, could I do it from memory? I have an adapted CloudFormation template for a private class C network, which is all I really need. However, I watched a [re:invent video on VPC design](https://www.youtube.com/watch?v=3Gv47NASmU4&t=3239s) and figured “why not use 65k IPs if they are free?” You never know, I might need a bigger network space one day, and it would be a pain to renumber it all.

So, the plan:  
My region has three AZs, so three public subnets, for the day I might actually add a load balancer and scaling group. Fun for another day. I also created 3 private subnets:

10.0.1.0/24 – public-2a  
10.0.2.0/24 – public-2b  
10.0.3.0/24 – public-2c  
10.0.100.0/24 – private-2a  
10.0.101.0/24 – private-2b  
10.0.102.0/24 – private-2c

I did have a moment of fun and created a 10.0.0.0/22 and revelled in all the room, but figured I could always redo the subnets later. 251 IPs is enough when I have one server instance and one database. I can dream big later.

First step, go to the console and create my first VPC. I didn’t realize until I saw a [re:invent video on how the network works on the actual machine](https://www.youtube.com/watch?v=St3SE4LWhKo&t=1807s) that I can have separate VPCs with the same CIDR blocks. Coming from a Cisco switching understanding of lans and vlans, it blew my mind that the VPC ID is just a tag added to the traffic to keep it separate from the rest of the bits and bytes. Still cleaning up bits of brain. Whoa.

Next step was to create the Internet GateWay (IGW) and attach it to my new VPC.

Next step was to create the routing table and associate the subnets with it. Right out of the gate, adding the 0.0.0.0/0 route and pointing it at the IGW. Wait a minute, now all the subnets can route out to the internet, how is that even private? This is where our friends the NAT instance and the NAT gateway come in. Ideally, creating the NAT gateway is the right answer, since it scales and doesn’t need managing or securing. However, it costs money, and I don’t see a need to patch servers in the private subnets right now, because I don’t have any. So, a NAT instance from the community AMI worked fine, I spun it up, changed the Source Destination Checks and gave it an Elastic IP. So far, so good.

Next, I created a new routing table with the NAT instance as the gateway. It popped right up as an option, didn’t have to look for it. Once I had the two routing tables, I assigned the public subnets to the main gateway and the private subnets to the NAT instance gateway, and then shut it down.

Almost there! I created a webDMZ security group that tightened down the access to the web server instance, and created a privateToPublic group that allowed only traffic from the webDMZ. Next, I spun up a test instance in a private subnet and installed mysql to test connectivity. Of course, I had to restart the NAT instance to allow the install.

I had a little trouble figuring out why the mysql traffic wasn’t working between the public and private subnets. I understood that subnets in the same VPC could communicate with each other, but I had to explicitly add mysql to the  the security group rules for each security group to reach each other, as well as explicitly add the public subnets to the the private subnet Access Control List (ACL). I need to go back and understand that better.

The fun part was getting the database in RDS to work, as AWS introduced a new interface and I had some fun with Subnet Groups and Security Groups, but that is another story for another day.

So, my personal account is divested from the default VPC, so I feel like my toy box is all cleaned up and put away properly.