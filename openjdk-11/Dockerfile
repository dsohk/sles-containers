FROM registry.suse.com/suse/sle15:15.1
LABEL maintainer="SUSE CaaSP and CAP - Sample Apps"

# -------------------------------------------------------------------------------

ARG repo
ARG cert

RUN echo "$cert" > /etc/pki/trust/anchors/RHN-ORG-TRUSTED-SSL-CERT.pem
RUN update-ca-certificates
RUN echo "$repo" > /etc/zypp/repos.d/susemanager:dockerbuild.repo

# -------------------------------------------------------------------------------

# All repos are ready
# Start my own docker build below

RUN zypper refs && zypper refresh
RUN zypper --non-interactive in java-11-openjdk

ENV JAVA_HOME=/usr/lib64/jvm/java
ENV PATH="$JAVA_HOME/bin:/usr/local/bin:/usr/bin:/bin"

CMD ["/bin/bash", "-c", "cat /etc/os-release"]

