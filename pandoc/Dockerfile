FROM alpine:3.11 as build

WORKDIR /var/tmp
ENV VER 2.9.1.1
ENV URL https://github.com/jgm/pandoc/releases/download/${VER}/pandoc-${VER}-linux-amd64.tar.gz
ADD ${URL} pandoc.tgz
RUN tar -xzf pandoc.tgz \
  && mv pandoc-${VER} pandoc

FROM alpine:3.11 as runner

LABEL "maintainer"="Mark Ayers <mark@philoserf.com>"
LABEL "repository"="https://github.com/philoserf/actions"
LABEL "homepage"="https://github.com/philoserf/actions/tree/master/pandoc"
LABEL "com.github.actions.name"="pandoc"
LABEL "com.github.actions.description"="https://pandoc.org"
LABEL "com.github.actions.color"="yellow"
LABEL "com.github.actions.icon"="check"

COPY --from=build /var/tmp/pandoc/bin/ /usr/bin/
COPY --from=build /etc/ssl/cert.pem /etc/ssl/certs/ca-certificates.crt

ENTRYPOINT ["pandoc"]
CMD ["--help"]

# Example:
#
# docker run \
#   --volume $PWD:$PWD \
#   --workdir $PWD \
#   --interactive \
#   --tty \
#   --rm \
#   philoserf/pandoc \
#     --from=markdown \
#     --to=gfm \
#     --wrap=none \
#     --output=README.md \
#     README.md
