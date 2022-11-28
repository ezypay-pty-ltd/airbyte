FROM airbyte/integration-base-java:dev AS build

WORKDIR /airbyte

ENV APPLICATION source-mssql

COPY build/distributions/${APPLICATION}*.tar ${APPLICATION}.tar

RUN tar xf ${APPLICATION}.tar --strip-components=1 && rm -rf ${APPLICATION}.tar

FROM airbyte/integration-base-java:dev

WORKDIR /airbyte

ENV APPLICATION source-mssql

COPY --from=build /airbyte /airbyte

RUN sed -i 's/jdk.tls.disabledAlgorithms=SSLv3, TLSv1, TLSv1.1,/jdk.tls.disabledAlgorithms=SSLv3,/' /usr/lib/jvm/java-17-amazon-corretto/conf/security/java.security

LABEL io.airbyte.version=0.4.25
LABEL io.airbyte.name=airbyte/source-mssql
