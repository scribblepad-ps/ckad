FROM busybox:musl

RUN mkdir app
WORKDIR /app

COPY ./run.sh /app/run.sh
RUN chmod +x /app/run.sh
USER  1001
CMD ["/bin/sh","/app/run.sh"]
