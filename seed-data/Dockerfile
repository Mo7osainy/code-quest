FROM alpine:3.16

RUN apk add --no-cache python3 apache2-utils

WORKDIR /app

COPY . .

RUN chmod +x generate-votes.sh && python3 make-data.py

RUN adduser -S -s /bin/false -u 1001 seeduser && chown -R seeduser /app

USER seeduser

CMD ["./generate-votes.sh"]

