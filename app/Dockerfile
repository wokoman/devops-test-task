FROM golang:alpine as builder
RUN mkdir /build/
ADD . /build/
WORKDIR /build/
RUN go build
FROM alpine
RUN adduser -S -D -H -h /app/ appuser
USER appuser
COPY --from=builder /build/ /app/
WORKDIR /app/
EXPOSE 8080
ENTRYPOINT ["./ervcp"]