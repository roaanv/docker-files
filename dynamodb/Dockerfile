FROM rvos-java8-ubuntu1604

# Create working space
RUN mkdir /var/dynamodb/wd
RUN mkdir /var/dynamodb/data
RUN mkdir /var/tmp

WORKDIR /var/dynamodb/wd

# Default port for DynamoDB Local
EXPOSE 8000

RUN /usr/bin/curl -o /var/tmp/dynamodb.tgz -L http://dynamodb-local.s3-website-us-west-2.amazonaws.com/dynamodb_local_latest
RUN /bin/tar -xfz /var/tmp/dynamodb.tgz /var/dynamodb/wd

# Default command for image
ENTRYPOINT ["/usr/bin/java", "-Djava.library.path=.", "-jar", "DynamoDBLocal.jar", "-dbPath", "/var/dynamodb_local"]
CMD ["-port", "8000"]

# Add VOLUMEs to allow backup of config, logs and databases
VOLUME ["/var/dynamodb/data", "/var/dynamodb/wd"]