FROM alpine:3.8 as base

RUN apk --no-cache add curl \
    && echo "Pulling watchdog binary from Github." \
    && curl -sSL https://github.com/openfaas/faas/releases/download/0.13.0/fwatchdog > /usr/bin/fwatchdog \
    && chmod +x /usr/bin/fwatchdog

FROM perl:5.28.2-slim

COPY --from=base /usr/bin/fwatchdog /usr/bin/
RUN cpanm Carton

RUN useradd -m app && usermod -G app app

COPY cpanfile .
COPY main.pl .
RUN carton install

COPY function function

RUN chown app:app -R /home/app
USER app
WORKDIR /home/app/

ENV fprocess="carton exec perl main.pl"

HEALTHCHECK --interval=5s CMD [ -e /tmp/.lock ] || exit 1
CMD ["fwatchdog"]
