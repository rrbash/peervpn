# peervpn
The open source peer-to-peer VPN
https://peervpn.net/tutorial/
Tutorial

 

Introduction

This Tutorial explains how to build a simple PeerVPN network that consists of two Linux machines. It is assumed that you already have installed PeerVPN on these two machines, which will be called "Node A" and "Node B" from now on.

 

Configuration of node A

Create the peervpn.conf of Node A with the following content:

port 7000
networkname ExampleNet
psk mysecretpassword
enabletunneling yes
interface peervpn0
ifconfig4 10.8.0.1/24

This will open UDP port 7000 and create a virtual ethernet interface with the name peervpn0 and the IP address 10.8.0.1.

Please note that Node A needs to be directly reachable from Node B and any further nodes that you will add to the network.

 

Configuration of node B

Create the peervpn.conf of Node B with the following content:

port 7000
networkname ExampleNet
psk mysecretpassword
enabletunneling yes
interface peervpn0
ifconfig4 10.8.0.2/24
initpeers node-a.example.com 7000

Replace node-a.example.com with the real address of Node A.

 

Testing the configuration

To test if everything works, start PeerVPN on both nodes. Each node should now have created its own peervpn0 interface. It may take some time until the VPN tunnel is built. Try to ping 10.8.0.2 from Node A or ping 10.8.0.1 from Node B. If you get a response, the VPN has been set up successfully!

 

Adding more nodes to the VPN

Copy the peervpn.conf of Node B to the new node and change the IP address in the ifconfig command to 10.8.0.3, 10.8.0.4, and so on. If you start the node, there will be a tunnel to Node A first. After some time, tunnels to Node B and all other nodes should be automatically built.

 
