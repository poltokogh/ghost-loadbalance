FROM haproxy:latest

# Copy config file
COPY haproxy.cfg /usr/local/etc/haproxy/haproxy.cfg

# Expose port
EXPOSE 80
EXPOSE 443
EXPOSE 8404
CMD ["haproxy", "-f", "/usr/local/etc/haproxy/haproxy.cfg"]
