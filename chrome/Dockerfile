FROM ubuntu:22.04

RUN apt-get update && apt-get install -y wget gnupg
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \ 
    && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list

RUN apt-get update && apt-get install -y xvfb xfonts-100dpi xfonts-75dpi xfonts-base google-chrome-stable

ENV DISPLAY=:99


EXPOSE 9222
# Create a virtual display
RUN Xvfb :99 -screen 0 1280x1024x16 &



# Start Chrome in headless mode
CMD ["google-chrome", "--headless", "--no-sandbox", "--disable-setuid-sandbox", "--disable-gpu", "--remote-debugging-port=9222", "--window-size=1280,1024"]
