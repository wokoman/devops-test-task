# Compile the Go app using Alpine Golang image
FROM golang:alpine as builder
RUN mkdir /build/
ADD . /build/
WORKDIR /build/
RUN go build
# Create clean image without build runtime
FROM alpine
# Create user to run the app under
RUN adduser -S -D -H -h /app/ appuser
USER appuser
COPY --from=builder /build/ /app/
WORKDIR /app/
EXPOSE 8080
ENTRYPOINT ["./ervcp"]