# Builder stage
FROM python:3 AS builder

RUN apt-get update && \
    apt-get install -y --no-install-recommends android-tools-adb && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY medusa/requirements.txt /app/medusa/requirements.txt
RUN pip3 install --no-cache-dir -r /app/medusa/requirements.txt

# Final stage
FROM python:3

RUN apt-get update && \
    apt-get install -y --no-install-recommends android-tools-adb && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY --from=builder /usr/local/lib/python3.*/site-packages/ /usr/local/lib/python3.*/site-packages/
COPY --from=builder /usr/local/bin /usr/local/bin

COPY medusa /app/medusa
COPY run_medusa.sh /app/run_medusa.sh

CMD ["bash", "/app/run_medusa.sh"]