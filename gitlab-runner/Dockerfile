FROM gitlab/gitlab-runner:ubuntu

# Install dependencies
RUN apt-get update && apt-get install -y curl unzip libc6 libstdc++6 iputils-ping

# Install OpenJDK 17
RUN apt-get install -y openjdk-17-jdk

# Install Node.js 20
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt-get install -y nodejs

# Download and install Sonar Scanner
RUN curl -L -o /tmp/sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-6.2.1.4610-linux-x64.zip \
    && ls -l /tmp/sonar-scanner.zip \
    && unzip /tmp/sonar-scanner.zip -d /opt \
    && ls -l /opt \
    && mv /opt/sonar-scanner-6.2.1.4610-linux-x64 /opt/sonar-scanner \
    && ln -s /opt/sonar-scanner/bin/sonar-scanner /usr/local/bin/sonar-scanner \
    && rm -rf /tmp/sonar-scanner.zip

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Set environment variables
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV SONAR_JAVA_HOME=$JAVA_HOME
ENV PATH=$JAVA_HOME/bin:$PATH
ENV SONAR_SCANNER_SKIP_JRE_PROVISIONING=true
ENV SONAR_SCANNER_SKIP_NODE_PROVISIONING=true

# Add a custom entrypoint script to configure Git
# COPY entrypoint.sh /entrypoint.sh
# RUN chmod +x /entrypoint.sh

# ENTRYPOINT ["/entrypoint.sh"]