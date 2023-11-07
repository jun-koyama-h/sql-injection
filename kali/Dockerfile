FROM kalilinux/kali-rolling:latest

# Update and install necessary packages
RUN apt-get update && apt-get install -y \
    sqlmap \
    # metasploit-framework \
    # nmap \
    # nikto \
    # dirb \
    # hydra \
    # john \
    # hashcat \
    # tcpdump \
    # git \
    && rm -rf /var/lib/apt/lists/*

CMD ["/bin/bash"]
