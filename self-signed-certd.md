update-ca-certificates --fresh
openssl s_client -showcerts -verify 5 -connect ghcr.io:443 < /dev/null 2>/dev/null | openssl x509 -outform PEM | tee ~/ghcr.io.crt
cp ~/ghcr.io.crt /usr/local/share/ca-certificates/
update-ca-certificates
