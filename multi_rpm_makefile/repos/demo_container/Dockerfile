FROM centos:7
COPY */*.rpm /tmp/rpms/
RUN yum install -y epel-release && \
    yum -v repolist enabled && \
    yum install -y \
        uwsgi \
        uwsgi-plugin-python \
        /tmp/rpms/python2-hello_lib-*.rpm \
        /tmp/rpms/python2-demo_app-*.rpm && \
    yum clean all -y && \
    rpm -q \
        uwsgi \
        uwsgi-plugin-python \
        python2-hello_lib \
        python2-demo_app
USER 1001
EXPOSE 8000 9191
ENTRYPOINT ["/usr/sbin/uwsgi", "--plugin", "python,http", "--http", ":8000", "--module", "demo_app:app", "--master", "--processes", "4", "--threads", "2", "--stats", ":9191"]
