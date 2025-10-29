FROM haproxy:latest

# Copy config file
COPY haproxy.cfg /usr/local/etc/haproxy/haproxy.cfg

# Copy cert
COPY haproxy-origin.pem /usr/local/etc/ssl/haproxy-origin.pem

# Expose port
EXPOSE 80
EXPOSE 443
EXPOSE 8404
CMD ["haproxy", "-f", "/usr/local/etc/haproxy/haproxy.cfg"]
