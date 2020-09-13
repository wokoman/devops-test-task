# Compile the Go app using Alpine Golang image
FROM golang:alpine as builder
RUN mkdir /build/
ADD . /build/
WORKDIR /build/
RUN go build

# Create clean image without build runtime
FROM alpine
# Set ARG and ENVs for using CI/CD variables
ARG LISTEN_PORT
ARG REDIS_HOST
ARG REDIS_PORT
ARG REDIS_PW
ENV ERVCP_PORT=$LISTEN_PORT
ENV ERVCP_DB_HOST=$REDIS_HOST
ENV ERVCP_DB_PORT=$REDIS_PORT
ENV ERVCP_DB_PW=$REDIS_PW
# Create user to run the app under
RUN adduser -S -D -H -h /app/ appuser
USER appuser
COPY --from=builder /build/ /app/
WORKDIR /app/
EXPOSE 8080
ENTRYPOINT ["./ervcp"]