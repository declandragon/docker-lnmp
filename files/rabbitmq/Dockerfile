FROM rabbitmq:3-management

LABEL declandragon="https://github.com/declandragon"

# set timezome
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone