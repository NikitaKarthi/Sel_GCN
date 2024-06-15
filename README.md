# Sel_GNN

This repository contains the supporting code for all the work that appears in the Sel_GNN paper. 

## Overview
Since the advent of computer networking, packet routing decisions have been extensively explored in academia. In today's deep learning era, the incorporation of neural networks into various supervised and unsupervised learning tasks has been proven highly successful. Packet routing is no exception to this assertion. Packet routing shares a similar structure to many autonomous control theory problems (such as maintaining the flight of a drone) and hence Reinforcement learning (RL) and Deep Q networks have been used before to assist in increasing **throughput** and decreasing **latency**, like in [2] by Modi et.al. Furthermore, Graph Neural Networks (GNNs), specially designed neural networks designed to operate over graphs, have also shown dominance in the field because networks are, in their fundamental form, graphs. Jiang et.al. in [1] have combined these two machine learning mechanisms to produce DGN: Deep Graph Neural networks. 

Our work is an extension of [1] and [2]. We implement Sel_GNN: An intelligent routing framework in multi-hop wireless networks. We complement the mentioned work by implementing selectivity at each agent using a distance heuristic to ensure that packets are routed even more efficiently, without circumnavigating/looping around the network. Our work is tested in a Jupyter notebook-based simulator. 
***

## Table of hyperparameters used in the code 

| hyperparameter | Description | Value |
| --- | --- | --- |
| seed | Random seed | 0 |
| n | Number of Rows | 10 |
| m | Number of columns | 10 | 
| n_nodes | Total number of nodes | 100 |
| k | Number of neighbors to drop | varies from 0 to 7 | 
| action_space | action space of each agent | 8 - k | 
| len_feature | node observation length | 2(8 - k) + 2 | 
| def_ttl | Base TTL | 1000 | 
| iot_rate | Rate of packet generation by IOT node | 20 |
| iot_generate_time | Gap between packet generation | 10 |
| create_packets_till | Last send time step in each episode | 400 | 
| epsilon | Greedy Probability | 0.3 | 
| gamma | Discount factor | 0.98 | 
| capacity | Replay buffer capacity | 200000 | 
| tau | Soft Update coefficient | 0.01 | 
| batch_size | Minibatching size | 8 | 
| lr | Learning rate | 0.001 | 
| num_ep | Number of training episodes | 1 | 
| num_of_eval_episodes | Number of evaluation episodes | 10 | 
| num_of_pretrain_episodes | Time steps to fill the buffer | 400 | 
| num_steps | Number of time steps per episode | 2000 | 


## Requirements
1. Python 3.12.2 - This is the version used in the original work. You may choose to use an older version but please check for package version conflicts.
2. All the packages listed in [dependencies.txt](https://github.com/HayagreevJ24/Sel_GCN/blob/main/Sel_GCN_Dependencies.txt)
3. A CPU/GPU/TPU capable of training the models from scratch for several hours at a time, if you plan on doing so. (We do not recommend using a cloud computing platform like Google Colab unless you have a subscription that allows you to train models for >= 8 hours at a time as the kernel unexpectedly terminates otherwise.) We used a 12th Gen Intel® Core™ i5-12450H × 12 cores running Ubuntu 22.04.4 LTS, 64-bit, with 16 gibibytes of system memory. 

Please use the following command to clone the repository and install the required packages: 
```bash
git clone Sel_GCN
cd Sel_GCN
python3 pip install Sel_GCN_Dependencies.txt
python3 jupyter notebook
```

## Code structure: 

1. [src](https://github.com/NikitaKarthi/Sel_GCN/tree/main/src)<br>
   This folder contains the code that defines the behaviour of the different node classes in the network. Additionally, it also contains code for the behaviour of the map as a whole and some utilities. The documentation for all classes here is present in the file [Code documentation - src.pdf](https://github.com/HayagreevJ24/Sel_GCN/blob/main/Code%20documentation%20-%20src.pdf)
   
2. [results_GNN_10_10_0.ipynb](https://github.com/NikitaKarthi/Sel_GCN/tree/main/results_GNN_10_10_0), [results_GNN_10_10_1.ipynb](https://github.com/NikitaKarthi/Sel_GCN/blob/main/results_GNN_10_10_1.ipynb), [results_GNN_10_10_2.ipynb](https://github.com/NikitaKarthi/Sel_GCN/blob/main/results_GNN_10_10_2.ipynb)<br>
   These are the main notebooks used to train and evaluate on three maps: 0, 1, and 2.

3. [Maps/maps_10_10](https://github.com/NikitaKarthi/Sel_GCN/tree/main/Maps/maps_10_10)<br>
   Contains the serialized pickle maps 0, 1, and 2.

4. [Plots](https://github.com/NikitaKarthi/Sel_GCN/tree/main/Plots)<br>
   Contains the plots produced from the code evidencing the performance of Sel_GNN.<br>
   (a) [Comparative Performance of Three Different Methods (Packets Received).png](https://github.com/NikitaKarthi/Sel_GCN/blob/main/Plots/Comparitive%20Performance%20of%20Three%20Different%20Methods%20(Packets%20Received).png) - Compares [1], [2], and Sel_GCN in terms of throughput (packets received on each map)<br>
   (b) [Comparative Performance of Three Different Methods (TTL).png](https://github.com/NikitaKarthi/Sel_GCN/blob/main/Plots/Comparitive%20Performance%20of%20Three%20Different%20Methods%20(TTL).png) - Compares [1], [2], and Sel_GCN in terms of latency (TTL of packets that arrive at the base station)<br>
   (c) [Performance of Sel_GCN based on Packets Received by the Base Station.png](https://github.com/NikitaKarthi/Sel_GCN/blob/main/Plots/Performance%20of%20Sel_GCN%20based%20on%20Packets%20Received%20by%20the%20Base%20Station.png) - Plot of number of packets received against the value of k for all 3 maps.<br>
   (d) [Performance of Sel_GCN based on TTL of Packets Received by the Base Station.png](https://github.com/NikitaKarthi/Sel_GCN/blob/main/Plots/Performance%20of%20Sel_GCN%20based%20on%20TTL%20of%20Packets%20Received%20by%20the%20Base%20Station.png) - Plot of incoming TTL of received packets against value of k for all 3 maps.<br>
   (e) [Results.ipynb](https://github.com/NikitaKarthi/Sel_GCN/blob/main/Plots/Results.ipynb) - Code used to produce and save all the plots.

5. [results_GNN_10_10_0](https://github.com/NikitaKarthi/Sel_GCN/tree/main/results_GNN_10_10_0), [results_GNN_10_10_1](https://github.com/NikitaKarthi/Sel_GCN/tree/main/results_GNN_10_10_1), [results_GNN_10_10_2](https://github.com/NikitaKarthi/Sel_GCN/tree/main/results_GNN_10_10_2)<br>
   Contain the log files, final and interim models (at different step numbers) as pytorch objects, arrays of packets received and TTL as pickle objects produced in (2) of this list. Compiled separately for each k value from 1 to 7.


## References: 
This code is based on
- [1] https://github.com/PKU-RL/DGN - (Jiechuan Jiang, Chen Dun, Tiejun Huang, and Zongqing Lu. Graph convolutional reinforcement learning. ICLR'20)
- [2] https://github.com/rishi1001/MARL-Packet-Router - (Modi, A., Shah, R., Jain, K., Verma, R., Shorey, R., & Saran, H. Multi-Agent Packet Routing (MAPR): Co-Operative Packet Routing Algorithm with Multi-Agent Reinforcement Learning)
