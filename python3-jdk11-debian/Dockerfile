FROM bitnami/python:3.7

# Python
RUN echo "PYTHON_VERSION" && python --version

# JDK
RUN apt-get update && \
	apt-get install java-common && \
	wget https://d3pxv6yz143wms.cloudfront.net/11.0.3.7.1/java-11-amazon-corretto-jdk_11.0.3.7-1_amd64.deb && \
	dpkg -i java-11-amazon-corretto-jdk_11.0.3.7-1_amd64.deb && \
	rm -rf /var/lib/apt/lists/*

RUN echo "JAVA_VERSION" && java -version
RUN echo "JAVAC_VERSION" && javac -version

# MAVEN
ENV MAVEN_VERSION 3.6.1
RUN curl -f -L http://central.maven.org/maven2/org/apache/maven/apache-maven/$MAVEN_VERSION/apache-maven-$MAVEN_VERSION-bin.tar.gz | tar -C /opt -xzv
ENV M2_HOME /opt/apache-maven-$MAVEN_VERSION
ENV maven.home $M2_HOME
ENV M2 $M2_HOME/bin
ENV PATH $M2:$PATH

RUN echo "MAVEN_VERION" && mvn -version

# PYTHON LIBS
RUN echo "PIP_VERSION" && pip --version

COPY requirements.txt /requirements.txt
RUN pip install -r /requirements.txt

RUN echo "PIP_LIBRARIES" && pip freeze

CMD ["python3"]
