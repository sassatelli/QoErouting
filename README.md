Code for solving the QoE-aware routing problem as the network evolves. The code can be called by ns3 to admit            
a new demand, reconfigure the network according to its status and 
the QoE experiend by e2e connections [1].                         
                                                                  
Created by                                                         
 - Paris Reseach Center, Huawei Technologies Co. Ltd.               
 - Laboratoire d'Informatique, Signaux et Systèmes de               
   Sophia Antipolis (I3S), Universite Cote d'Azur and CNRS           
                                                                   
Contributors:                                                      
- Giacomo CALVIGIONI (I3S)                                         
- Ramon APARICIO-PARDO (I3S)                                       
- Lucile SASSATELLI (I3S)                                          
- Jeremie LEGUAY (Huawei)                                          
- Stefano PARIS (Huawei)                                           
- Paolo MEDAGLIANI (Huawei)                                        
                                                                    
References:                                                        
[1] Giacomo Calvigioni, Ramon Aparicio-Pardo, Lucile Sassatelli,   
     Jeremie Leguay, Stefano Paris, Paolo Medagliani,               
     "Quality of Experience-based Routing of Video Traffic for      
      Overlay and ISP Networks". In the Proceedings of the IEEE     
     International Conference on Computer Communications            
      (INFOCOM), 15-19 April 2018.                                  
                                                                  
Contacts:                                                          
- For any question please use the address: qoerouting@gmail.com    


Acknowledgements
================
When writing a paper that uses this Code, we would appreciate it if you could cite both the authors of this code and of the initial AMust project itself (https://github.com/ChristianKreuzberger/AMuSt-Simulator/). 
The citations would look like:
- G. Calvigioni, R. Aparicio-Pardo, L. Sassatelli, J. Leguay, S. Paris and P. Medagliani. Quality of Experience-based Routing of Video Traffic for Overlay and ISP Networks.IEEE International Conference on Computer Communications (INFOCOM), Honolulu, HI, USA, Apr. 2018.  
- C. Kreuzberger, D. Posch, and H. Hellwagner, “AMuSt Framework - Adaptive Multimedia Streaming Simulation Framework for ns-3 and ndnSIM,” 2016.

In addition to AMust, the code contains the following contributions:
- Loading of streaming scenarios (network parameters, installation of streaming servers and clients, streaming parameters) 
- Routing management for each streaming sessions (SDN like routing using reconfiguratble static routes from an SDN routing solver)
- Routing solver implementing various algorithms in MAtlab (sub-gradient based heuristic, ILP, ssucessive shortest path)
- QoE functions for representative content types (high motion, low motion, etc)
- QoE and QoS statictics retreival

Compile and run
================
Go to AMuSt-ns3-master directory
Execute ./waf configure --with-dash=../AMuSt-libdash-master/libdash/ --enable-examples
Execute ./waf build
Test execution in "scratch" directory: ../waf --run "dash-simulator"    

NS3 Files (in NS3 scratch directory):
- dash-demo.cc: demo file adapted from the Amust project (scenario parameters are hard coded, no routing)
- dash-simulator.cc: can read sscenario from files, no rerouting
- dash-simulator.cc: can read sscenario from files, QoE-based routing
- file-simulator.cc: used to evaluate interfence beween file transfers and DASH streaming
DASH-enabled clients and server code can be found in "src/applications/model/"

SCRIPTS (in NS3 scratch directory):
- analyze.sh: retreive statics from simulation (static scenario)
- analyze-rerouting.sh: retreive statics from simulation (dynamic scenario - with rerouting)
- analyze-speed.sh: analyze downloading rates
- launch-bottleneck.sh: launch simulations with static scenarios
- launch-rerouting.sh: launch simulations with dynamic scenarios

MATLAB files (in matlab directory):
- see README.txt in AMuSt-ns3-master/../matlab

Simulation Inputs:
- content/scenario/nodes: description of nodes with their types (router, client, server)
- content/scenario/adj_matrix: adjacency matrix of the network with QoS caracteristics of links
- content/scenario/requests: streaming requests with start and stop times, content id, etc.
- content/representations/: directory containing representations for all contents

Simulation Outputs
- AMuSt-ns3-master/demo.tr: TR file from NS3
- AMuSt-ns3-master/FlowMonitor.xml report from FlowMon module in NS3
- AMuSt-ns3-master/report.csv: report from libdash module
- AMuSt-ns3-master/segments: list of segments
- AMuSt-ns3-master/addresses: mapping between nodes and IP addresses
- Standard output of NS3: typically stored in scratch/log.txt
