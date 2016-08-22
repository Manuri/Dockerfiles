FROM ubuntu:trusty

RUN \
useradd -m -d /home/jenkins -s /bin/sh jenkins \
&& echo "jenkins:jenkins" | chpasswd

RUN \ 
apt-get -q update && apt-get install -y openssh-server software-properties-common git \
&& apt-get clean \
&& mkdir /var/run/sshd

RUN \
mkdir -p /build/software/maven \
&& wget -P /build/software/maven https://archive.apache.org/dist/maven/maven-3/3.0.5/binaries/apache-maven-3.0.5-bin.tar.gz \
&& tar -xvzf /build/software/maven/apache-maven-3.0.5-bin.tar.gz --directory /build/software/maven \
&& rm /build/software/maven/apache-maven-3.0.5-bin.tar.gz

RUN \
wget -P /build/software/maven https://archive.apache.org/dist/maven/maven-3/3.3.3/binaries/apache-maven-3.3.3-bin.tar.gz \
&& tar -xvzf /build/software/maven/apache-maven-3.3.3-bin.tar.gz --directory /build/software/maven \
&& rm /build/software/maven/apache-maven-3.3.3-bin.tar.gz

RUN \
wget -P /build/software/maven https://archive.apache.org/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz \
&& tar -xvzf /build/software/maven/apache-maven-3.3.9-bin.tar.gz --directory /build/software/maven \
&& rm /build/software/maven/apache-maven-3.3.9-bin.tar.gz

RUN \
echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections \
&& add-apt-repository -y ppa:webupd8team/java \
&& apt-get update \
&& apt-get install -y oracle-java8-installer \
&& apt-get clean \
&& rm -rf /var/cache/oracle-jdk8-installer

RUN \
echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections \
&& add-apt-repository -y ppa:webupd8team/java \
&& apt-get update \
&& apt-get install -y oracle-java7-installer \
&& apt-get clean \
&& rm -rf /var/cache/oracle-jdk7-installer

RUN apt-get install -y openjdk-7-jdk && apt-get clean

RUN \
add-apt-repository ppa:openjdk-r/ppa -y \
&& apt-get update && apt-get install -y openjdk-8-jdk \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
