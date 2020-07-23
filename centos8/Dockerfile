FROM centos:latest

RUN yum clean all

RUN yum update -y

RUN yum install -y epel-release

RUN yum groupinstall -y "Development tools"

RUN yum install -y ansible tree vim groff-base jq sudo python36 python3-devel python3-pip krb5-devel

ARG NEW_USER=mikemcfarlane

RUN useradd -ms /bin/bash $NEW_USER \
    && echo "$NEW_USER ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/$NEW_USER \
    && chmod 0440 /etc/sudoers.d/$NEW_USER

RUN /usr/bin/pip3 install awscli \
    && /usr/bin/pip3 install pipenv
    
RUN mkdir -p /home/$NEW_USER/repos/ \
    && mkdir -p /home/$NEW_USER/.aws/

ENV PATH="/home/$NEW_USER/.local/bin:${PATH}"

# # python 3 fixes for default text encoding
# ENV LC_ALL="en_GB.utf8"
# ENV LANG=en_GB.utf8

ENV USER=$NEW_USER

ENV LOGNAME=$NEW_USER

EXPOSE 7001

USER $NEW_USER

WORKDIR /home/$NEW_USER

CMD ["/bin/bash"]