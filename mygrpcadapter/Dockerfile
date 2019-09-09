FROM golang:1.11 as builder
WORKDIR /go/src/github.com/username/myootadapter/
COPY ./ .
RUN CGO_ENABLED=0 GOOS=linux \
    go build -a -installsuffix cgo -v -o bin/mygrpcadapter ./mygrpcadapter/cmd/

FROM alpine:3.8
RUN apk --no-cache add ca-certificates
WORKDIR /bin/
COPY --from=builder /go/src/github.com/username/myootadapter/bin/mygrpcadapter .
ENTRYPOINT [ "/bin/mygrpcadapter" ]
CMD [ "8000" ]
EXPOSE 8000