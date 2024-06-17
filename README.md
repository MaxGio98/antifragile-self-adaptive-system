<h1>Engineering Antifragile Self-Adaptive Systems in Service-based Architecture</h1>
MSc final thesis project by Massimiliano Giovagnola.
##Project composition
This project is an Antifragile System made of the following components:
1. a [managed system](https://github.com/MaxGio98/antifragile-self-adaptive-system/tree/main/VulnerableNode) made of a set of Vulnerable Nodes susceptible to internal and external attacks;
2. a [managing system](https://github.com/MaxGio98/antifragile-self-adaptive-system/tree/main/Managing), which is responsible of adapting the managed system;
3. a [infection script](https://github.com/MaxGio98/antifragile-self-adaptive-system/blob/main/infector.py) that externally infects the vulnerable network.

##Installation guide
The whole Antifragile was developed, run and tested on a Lenovo Ideapad Gaming 3 15ARH05 with the following specifications:
- CPU: AMD Ryzen 7 4800H, 8 x 2.9 - 4.2 GHz cores
- GPU: NVIDIA GTX 1650Ti Mobile, 4 GB GDDR6 VRAM
- RAM: 32 GB DDR4 3200MHz
- Storage: 512 GB on NVMe SSD + 1 TB on 2.5" HDD
- OS: Ubuntu 23.10 Mantic Minotaur
- IDE: IntelliJ IDEA
- OpenJDK v. "22-ea", Docker v. 26.1.3, Python v. 3.11.6


In order to run the project, you will need to have both Docker and a JDK version greater than or equal to 21 pre-installed on your Linux computer.

The next step involves the creation of a GitHub repository (if you don’t have one yet). You can do so by forking [this repository](https://github.com/MaxGio98/antifragile-self-adaptive-system).

Next, you need to open a terminal in the "VulnerableNode" folder and create a Docker image of the Vulnerable Node, using the following command:

```
$ sudo docker build -t node -f ./DockerFile .
```

Then, with your IDE (preferably IntelliJ) run with sudo privileges, you can open the Managing Node project, contained in the "Managing" folder and decide to run it directly or by fistly creating a JAR.

If you want to run the program as a JAR, go to the folder that contains it and open a terminal and, then, execute it with this command:
```
$ sudo java -jar Managing-0.0.1-SNAPSHOT.jar
```
##Modify network characteristics
If you don't modify the default network characteristics, contained in the Managing's `application.properties` file, you will create 50 Vulnerable Nodes, with 10 neighbors on average and 5 vulnerability types.

If you're executing the Managing Node through IntelliJ, simply go to the "Managing/src/main/resources" folder and modify the content of `application.properties`.

If you want to modify it, but you've already created a JAR file, you can still modify the `application.properties` file:
- Extract `application.properties` from the JAR
```
$ sudo jar xf Managing-0.0.1-SNAPSHOT.jar BOOT-INF/classes/application.properties
```
- Modify the values
```
sudo vim BOOT-INF/classes/application.properties
```
-Overwrite the `application.properties` inside the JAR
```
$ sudo jar uf Managing-0.0.1-SNAPSHOT.jar BOOT-INF/classes/application.properties
```
##Python scripts
###Infector script
The `infector.py` file, located at the root of the folder, is the responsible for the creations of external attacks to the vulnerable network. After the Managing Node is launched and after the vulnerable network is then ready, you can execute it. If you want to create an homogenous attack, write, as the first argument -1 and, then, the probability value.
###graph.py
With this tool is possible to observe the network graphically, with an automatic refresh of 5 seconds.
A node is represented as a colored red or green (depending on its health status) circle, with on top its own IP address and vulnerability type value. A node is a neighbor of an another node if they share a link, i.e., there's a line that connects the two circles.

