# 開発環境
FROM golang:1.18-alpine

WORKDIR /api
COPY . .
ENV GO111MODULE=on

#RUN apt-get --allow-releaseinfo-change update && apt upgrade -y
RUN go install github.com/pilu/fresh@latest
ENV PATH $PATH:/go/pkg/mod/cache/download/github.com/pilu/
CMD ["fresh"]
