FROM ubuntu:16.04

RUN apt-get update && apt-get install -y git
COPY ./contents_cloner /contents_cloner 
RUN chmod a+x /contents_cloner
WORKDIR /
CMD ["/contents_cloner"]