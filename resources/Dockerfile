FROM ubuntu:22.10

#Install openssh-server
RUN apt update && apt install openssh-server sudo -y

#Create a group "paromgroup"
RUN groupadd paromgroup

#Create a user "parom"
RUN useradd -d /home/par -m -s /bin/bash -g paromgroup par
#Set default password 123 for user parom
RUN echo "123\n123" | passwd parom

#Create a user "evgen"
RUN useradd -d /home/evg -m -s /bin/bash -g paromgroup evg
#Set default password 321 for user evgen
#RUN echo "321\n321" | passwd evgen
#Create .ssh directory in evgen home directory
RUN mkdir -p /home/evg/.ssh/authorized_keys
#Copy the ssh public key in the authorized_keys file
#The id_rsa.pub below is a public key file you get from ssh-keygen
#They are under ~/.shh directory by default
COPY fordockerubuntu.pub /home/evg/.ssh/authorized_keys
#Change owership of the key file

#RUN sudo chown evgen /home/evgen/.shh/authorized_keys
RUN chgrp paromgroup /home/evg/.ssh/authorized_keys
#RUN chmod 648 /home/evgen/.ssh/authorized_keys

#Start SSH service
RUN service ssh start
#Expose docker port 22
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
