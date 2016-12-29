FROM roaanv/alpine-java8

# Create working space
RUN mkdir /var/dynamodb /var/dynamodb/wd /var/dynamodb/data

WORKDIR /var/dynamodb/wd

RUN wget -O /var/tmp/dynamodb.tgz http://dynamodb-local.s3-website-us-west-2.amazonaws.com/dynamodb_local_latest && \
  /bin/tar -xvf /var/tmp/dynamodb.tgz -C /var/dynamodb/wd && \
  rm /var/tmp/dynamodb.tgz

# Default port for DynamoDB Local
EXPOSE 8000

# Default command for image
ENTRYPOINT ["/usr/bin/java", "-Djava.library.path=.", "-jar", "DynamoDBLocal.jar", "-dbPath", "/var/dynamodb/data"]
CMD ["-port", "8000"]

# Add VOLUMEs to allow backup of config, logs and databases
VOLUME ["/var/dynamodb/data", "/var/dynamodb/wd"]
