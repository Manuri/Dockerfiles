FROM ubuntu:trusty

RUN \
useradd -m -d /home/jenkins -s /bin/sh jenkins \
&& echo "jenkins:jenkins" | chpasswd

RUN \ 
apt-get -q update && apt-get install -y openssh-server software-properties-common git ant curl unzip xvfb dbus-x11 \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* \
&& mkdir /var/run/sshd


RUN \
apt-get update \
&& apt-get --yes --force-yes install firefox \
&& apt-get --yes --force-yes install firefox=28.0+build2-0ubuntu2 \
&& apt-mark hold firefox \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*

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
&& rm -rf /var/lib/apt/lists/* \
&& rm -rf /var/cache/oracle-jdk8-installer \
&& mkdir -p /build/software/jce \
&& wget -P /build/software/jce --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jce/8/jce_policy-8.zip \
&& unzip -o /build/software/jce/jce_policy-8.zip -d /build/software/jce \
&& mv /usr/lib/jvm/java-8-oracle/jre/lib/security/local_policy.jar /usr/lib/jvm/java-8-oracle/jre/lib/security/local_policy-original.jar \
&& mv /usr/lib/jvm/java-8-oracle/jre/lib/security/US_export_policy.jar /usr/lib/jvm/java-8-oracle/jre/lib/security/US_export_policy-original.jar \
&& cp /build/software/jce/UnlimitedJCEPolicyJDK8/local_policy.jar /usr/lib/jvm/java-8-oracle/jre/lib/security/ \
&& cp /build/software/jce/UnlimitedJCEPolicyJDK8/US_export_policy.jar /usr/lib/jvm/java-8-oracle/jre/lib/security/ \
&& rm  /build/software/jce/jce_policy-8.zip \
&& rm -r /build/software/jce/UnlimitedJCEPolicyJDK8

RUN \
echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections \
&& add-apt-repository -y ppa:webupd8team/java \
&& apt-get update \
&& apt-get install -y oracle-java7-installer \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* \
&& rm -rf /var/cache/oracle-jdk7-installer \
&& wget -P /build/software/jce --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jce/7/UnlimitedJCEPolicyJDK7.zip \
&& unzip -o /build/software/jce/UnlimitedJCEPolicyJDK7.zip -d /build/software/jce \
&& mv /usr/lib/jvm/java-7-oracle/jre/lib/security/local_policy.jar /usr/lib/jvm/java-7-oracle/jre/lib/security/local_policy-original.jar \
&& mv /usr/lib/jvm/java-7-oracle/jre/lib/security/US_export_policy.jar /usr/lib/jvm/java-7-oracle/jre/lib/security/US_export_policy-original.jar \
&& cp /build/software/jce/UnlimitedJCEPolicy/local_policy.jar /usr/lib/jvm/java-7-oracle/jre/lib/security/ \
&& cp /build/software/jce/UnlimitedJCEPolicy/US_export_policy.jar /usr/lib/jvm/java-7-oracle/jre/lib/security/ \
&& rm /build/software/jce/UnlimitedJCEPolicyJDK7.zip \
&& rm -r /build/software/jce/UnlimitedJCEPolicy


RUN apt-get update && apt-get install -y openjdk-7-jdk && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN \
add-apt-repository ppa:openjdk-r/ppa -y \
&& apt-get update && apt-get install -y openjdk-8-jdk \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
