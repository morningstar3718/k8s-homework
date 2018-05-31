# build stage
FROM golang:alpine AS build-env
WORKDIR /go
COPY main.go /go/
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o main .
 
# final stage
FROM alpine
COPY --from=build-env /go/main /main
EXPOSE 5566
CMD ["/main"]

