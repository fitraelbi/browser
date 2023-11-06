FROM ubuntu:jammy

# COPY --from=go /root/.cache/rod /root/.cache/rod
# 
RUN touch /.dockerenv

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update > /dev/null && \
    apt install --assume-yes software-properties-common && \
    add-apt-repository ppa:mozillateam/ppa && \
    echo "Package: *\nPin: release o=LP-PPA-mozillateam\nPin-Priority: 1001" | tee /etc/apt/preferences.d/mozilla-firefox && \
    echo 'Unattended-Upgrade::Allowed-Origins:: "LP-PPA-mozillateam:${distro_codename}";' |  tee /etc/apt/apt.conf.d/51unattended-upgrades-firefox && \
    apt-get update > /dev/null && \
    apt-get install --no-install-recommends -y \
    firefox \
    # timezone
    tzdata \
    # process reaper
    dumb-init \
    # headful mode support, for example: $ xvfb-run chromium-browser --remote-debugging-port=9222
    xvfb \
    > /dev/null && \
    # cleanup
    rm -rf /var/lib/apt/lists/*

# process reaper
ENV DISPLAY=:1

CMD Xvfb :1 -screen 0 1024x768x24 & firefox --remote-debugging-port=9222

#ENTRYPOINT ["firefox", "--headles", "--remote-debugging-port=9222"]

#CMD  firefox --remote-debugging-port=9222

