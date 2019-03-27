FROM nginx:1.14

LABEL declandragon="https://github.com/declandragon"

# set timezome
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone