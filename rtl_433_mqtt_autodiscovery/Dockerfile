ARG BUILD_FROM=homeassistant/amd64-base-python:3.9-alpine3.16
FROM ${BUILD_FROM} as builder

ARG rtl433GitRevision=22.11

RUN wget https://raw.githubusercontent.com/mholgatem/rtl_433-hass-addons/mholgatem-patch-1/rtl_433_mqtt_autodiscovery/rtl_433_mqtt_hass.py -O rtl_433_mqtt_hass.py

FROM ${BUILD_FROM}

COPY --from=builder rtl_433_mqtt_hass.py .
COPY run.sh .

RUN \
    pip install \
        --no-cache-dir \
        --prefer-binary \
        paho-mqtt \
    \
    && chmod a+x /run.sh

CMD [ "/run.sh" ]
