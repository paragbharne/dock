FROM ubuntu:14.04
MAINTAINER pari

ENV CONF_HOME     /home/confluence
ENV CONFLUENCE_VERSION  6.0.1
ENV MYSQL_DRIVER_VERSION 5.1.40
ENV LANG ko_KR.UTF-8


RUN useradd --create-home --comment "Account for running Atlassian Confluence" confluence \
    && chmod -R a+rw ~confluence

RUN wget                    "http://www.atlassian.com/software/confluence/downloads/binary/atlassian-confluence-${CONFLUENCE_VERSION}.tar.gz" \
    && tar -xzf             "atlassian-confluence-${CONFLUENCE_VERSION}.tar.gz" \
    && rm                   "atlassian-confluence-${CONFLUENCE_VERSION}.tar.gz" \
    && mkdir -p             "/usr/local/atlassian" \
    && mv                   "atlassian-confluence-${CONFLUENCE_VERSION}" "/usr/local/atlassian/confluence" \
    && echo -e              "\nconfluence.home=$CONF_HOME" >> "/usr/local/atlassian/confluence/confluence/WEB-INF/classes/confluence-init.properties" \
    && chown -R confluence:confluence "/usr/local/atlassian/confluence" \
    && chmod -R 777         "/usr/local/atlassian/confluence/temp" \
    && chmod -R 777         "/usr/local/atlassian/confluence/logs" \
    && chmod -R 777         "/usr/local/atlassian/confluence/work" \
    && wget "http://cdn.mysql.com/Downloads/Connector-J/mysql-connector-java-${MYSQL_DRIVER_VERSION}.tar.gz" \
    && tar -xzf "mysql-connector-java-${MYSQL_DRIVER_VERSION}.tar.gz" \
    && mv "mysql-connector-java-${MYSQL_DRIVER_VERSION}/mysql-connector-java-${MYSQL_DRIVER_VERSION}-bin.jar" "/usr/local/atlassian/confluence/lib/." \
    && rm -rf "mysql-connector-java-${MYSQL_DRIVER_VERSION}.tar.gz" \
    && rm -rf "mysql-connector-java-${MYSQL_DRIVER_VERSION}" \
    && chown confluence:confluence "/usr/local/atlassian/confluence/lib/mysql-connector-java-${MYSQL_DRIVER_VERSION}-bin.jar" \
    && sed -i "s/Xms1024m/Xms128m/g" "/usr/local/atlassian/confluence/bin/setenv.sh"

# ?
ADD server.xml /usr/local/atlassian/confluence/conf/server.xml

# set the principal user as new non-root confluence account
USER confluence

# expose default ``Atlassian Confluence`` HTTP port
EXPOSE 8090

# set volume mount points for installation and home directory
VOLUME ["/home/confluence", "/usr/local/atlassian/confluence"]

# run ``Atlassian Confluence`` and as a foreground process by default
ENTRYPOINT ["/usr/local/atlassian/confluence/bin/start-confluence.sh"]
CMD ["-fg"]

