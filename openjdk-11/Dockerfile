FROM registry.suse.com/suse/sle15:15.1
LABEL maintainer="SUSE CaaSP and CAP - Sample Apps"

# -------------------------------------------------------------------------------

# Import TLS cert from SUSE SMT/RMT Server
# Uncomment the line below if you are using SMT Server
# ADD http://<SMT/RMT SERVER>/rmt.crt /etc/pki/trust/anchors/smt.crt
ADD http://rmt.suse.lab/rmt.crt /etc/pki/trust/anchors/smt.crt

# Import CA cert from SUSE Manager
# Comment the line below out if you are not using SUSE Manager in the docker host.
ADD cert/RHN-ORG-TRUSTED-SSL-CERT /etc/pki/trust/anchors/

# update CA cert
RUN update-ca-certificates

# Copy all SLES zypper repos into the container
ADD etc/ /etc/zypp/
RUN zypper refs && zypper refresh

# -------------------------------------------------------------------------------

# All repos are ready
# Start my own docker build below

RUN zypper --non-interactive in java-11-openjdk

ENV JAVA_HOME=/usr/lib64/jvm/java
ENV PATH="$JAVA_HOME/bin:/usr/local/bin:/usr/bin:/bin"

CMD ["/bin/bash", "-c", "cat /etc/os-release"]

