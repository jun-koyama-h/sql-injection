FROM nginx:1.25.3

RUN apt-get update \
  && apt-get install -y apt-utils autoconf \
    automake build-essential \
    git libcurl4-openssl-dev \
    libgeoip-dev liblmdb-dev \
    libpcre3-dev libtool \
    libxml2-dev libyajl-dev \
    pkgconf wget zlib1g-dev

WORKDIR /root
RUN git clone --depth 1 -b v3/master --single-branch https://github.com/SpiderLabs/ModSecurity \
  && cd ModSecurity && git submodule init && git submodule update
WORKDIR /root/ModSecurity
RUN ./build.sh && ./configure && make && make install

# ngx_http_modsecurity_module
RUN git clone --depth 1 https://github.com/SpiderLabs/ModSecurity-nginx.git \
  && wget http://nginx.org/download/nginx-1.25.3.tar.gz \
  && tar zxvf nginx-1.25.3.tar.gz
WORKDIR /root/ModSecurity/nginx-1.25.3
RUN ./configure --with-compat --add-dynamic-module=../ModSecurity-nginx && make modules \
  && cp /root/ModSecurity/nginx-1.25.3/objs/ngx_http_modsecurity_module.so /etc/nginx/modules
COPY nginx.conf /etc/nginx/nginx.conf

# SecRuleEngine
RUN mkdir -p /etc/nginx/modsecurity \
  && cp /root/ModSecurity/modsecurity.conf-recommended /etc/nginx/modsecurity/modsecurity.conf \
  && sed -i -e "s/SecRuleEngine DetectionOnly/SecRuleEngine On/g" /etc/nginx/modsecurity/modsecurity.conf
COPY conf.d/main.conf /etc/nginx/modsecurity
COPY conf.d/default.conf /etc/nginx/conf.d/default.conf
COPY conf.d/ruleset.conf /etc/nginx/modsecurity/ruleset.conf
RUN cp /root/ModSecurity/unicode.mapping /etc/nginx/modsecurity \
  && curl -OL https://github.com/coreruleset/coreruleset/archive/v3.3.0.tar.gz \
    && tar -xvzf v3.3.0.tar.gz \
    && mv coreruleset-3.3.0 coreruleset \
    && mv coreruleset /usr/local \
    && cp /usr/local/coreruleset/crs-setup.conf.example \ 
       /usr/local/coreruleset/crs-setup.conf

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]