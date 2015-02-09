FROM codearte/openjdk

RUN groupadd -g 2000 jira && useradd -d /home/jira -m -g 2000 -u 2000 jira

WORKDIR /home/jira

RUN wget http://downloads.atlassian.com/software/jira/downloads/atlassian-jira-6.3.15.tar.gz -O jira.tgz

RUN mkdir /home/jira/jira-app \
    && tar -xzf jira.tgz --strip 1 -C /home/jira/jira-app \
    && rm -r jira.tgz \
    && echo jira.home=/home/jira/jira-home > /home/jira/jira-app/atlassian-jira/WEB-INF/classes/jira-application.properties \
    && sed -i 's/path=""/path="\/jira"/g' /home/jira/jira-app/conf/server.xml \
    && mkdir /home/jira/jira-home \
    && chown jira: -R /home/jira

USER jira
VOLUME /home/jira/jira-home
EXPOSE 8080
ENTRYPOINT /home/jira/jira-app/bin/start-jira.sh -fg