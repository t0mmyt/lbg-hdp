FROM centos:6

ARG AMBARI_REPO_URL='http://public-repo-1.hortonworks.com/ambari/centos6/2.x/updates/2.6.1.0/ambari.repo'
ENV AMBARI_REPO_URL $AMBARI_REPO_URL

RUN yum install -y wget sudo net-tools
RUN wget -nv ${AMBARI_REPO_URL} -O /etc/yum.repos.d/ambari.repo
RUN yum install -y ambari-server postgresql-jdbc
RUN ambari-server setup --database=postgres --databasehost=postgres.lbg.dev --databaseport=5432 --databasename=ambari --postgresschema=ambari  --databaseusername=ambari --databasepassword=dev --silent
RUN ambari-server setup --jdbc-db postgres --jdbc-driver=/usr/share/java/postgresql-jdbc.jar
RUN yum install -y krb5-server krb5-libs krb5-workstation
RUN yum install -y ambari-agent
RUN yum install -y ambari-metrics-*
ADD scripts/start.sh /start.sh
ADD scripts/HDP-2.6.4.0-91.xml /tmp
ADD scripts/krb5.conf /etc/krb5.conf
CMD /start.sh
