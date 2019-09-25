FROM openfaas/classic-watchdog:0.18.0 as watchdog

FROM perl:5-slim

COPY --from=watchdog /fwatchdog /usr/bin/fwatchdog
RUN chmod +x /usr/bin/fwatchdog

RUN cpanm Carton

RUN useradd -m app && usermod -G app app
WORKDIR /home/app/

COPY cpanfile .
RUN carton install
COPY main.pl .
COPY function function

RUN chown app:app -R /home/app
USER app

ENV fprocess="carton exec perl main.pl"

HEALTHCHECK --interval=5s CMD [ -e /tmp/.lock ] || exit 1
CMD ["fwatchdog"]
