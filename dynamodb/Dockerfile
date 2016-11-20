FROM roaanv/java8-dev

# Create working space
RUN mkdir /var/dynamodb
RUN mkdir /var/dynamodb/wd
RUN mkdir /var/dynamodb/data

WORKDIR /var/dynamodb/wd

# Default port for DynamoDB Local
EXPOSE 8000

RUN wget -O /var/tmp/dynamodb.tgz http://dynamodb-local.s3-website-us-west-2.amazonaws.com/dynamodb_local_latest
RUN /bin/tar -xvf /var/tmp/dynamodb.tgz -C /var/dynamodb/wd
RUN rm /var/tmp/dynamodb.tgz

# Default command for image
ENTRYPOINT ["/usr/bin/java", "-Djava.library.path=.", "-jar", "DynamoDBLocal.jar", "-dbPath", "/var/dynamodb/data"]
CMD ["-port", "8000"]

# Add VOLUMEs to allow backup of config, logs and databases
VOLUME ["/var/dynamodb/data", "/var/dynamodb/wd"]