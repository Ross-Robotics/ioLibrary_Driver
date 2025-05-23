# Ethernet
add_library(ETHERNET_FILES STATIC
        Ethernet/socket.c
        Ethernet/wizchip_conf.c
)

if(${WIZNET_CHIP} STREQUAL W5100S)
target_include_directories(ETHERNET_FILES INTERFACE
        Ethernet
        Ethernet/W5100S
        )

target_link_libraries(ETHERNET_FILES PUBLIC
        W5100S_FILES
        )
elseif(${WIZNET_CHIP} STREQUAL W5500)
target_include_directories(ETHERNET_FILES INTERFACE
        Ethernet
        Ethernet/W5500
)

target_link_libraries(ETHERNET_FILES PUBLIC
        W5500_FILES
)
endif()

if(${WIZNET_CHIP} STREQUAL W5100S)
add_library(W5100S_FILES STATIC)

target_sources(W5100S_FILES PUBLIC
        Ethernet/W5100S/w5100s.c
        )

target_include_directories(W5100S_FILES INTERFACE
        Ethernet
        Ethernet/W5100S
        )

target_link_libraries(W5100S_FILES PRIVATE
        ETHERNET_FILES
        )
elseif(${WIZNET_CHIP} STREQUAL W5500)
add_library(W5500_FILES STATIC)

target_sources(W5500_FILES PUBLIC
        Ethernet/W5500/w5500.c
)

target_include_directories(W5500_FILES INTERFACE
        Ethernet
        Ethernet/W5500
)

target_link_libraries(W5500_FILES PRIVATE
        ETHERNET_FILES
)
endif()

# Loopback
add_library(LOOPBACK_FILES STATIC)

target_sources(LOOPBACK_FILES PUBLIC
        Application/loopback/loopback.c
)

target_include_directories(LOOPBACK_FILES PUBLIC
        Ethernet
        Application/loopback
)

# DHCP
add_library(DHCP_FILES STATIC)

target_sources(DHCP_FILES PUBLIC
        Internet/DHCP/dhcp.c
)

target_include_directories(DHCP_FILES PUBLIC
        Ethernet
        Internet/DHCP
)

# DNS
add_library(DNS_FILES STATIC)

target_sources(DNS_FILES PUBLIC
        Internet/DNS/dns.c
)

target_include_directories(DNS_FILES PUBLIC
        Ethernet
        Internet/DNS
)

# FTP Client
add_library(FTPCLIENT_FILES STATIC)

target_sources(FTPCLIENT_FILES PUBLIC
        Internet/FTPClient/ftpc.c
)

target_include_directories(FTPCLIENT_FILES PUBLIC
        Ethernet
        Internet/FTPClient
)

# FTP Server
add_library(FTPSERVER_FILES STATIC)

target_sources(FTPSERVER_FILES PUBLIC
        Internet/FTPServer/ftpd.c
)

target_include_directories(FTPSERVER_FILES PUBLIC
        Ethernet
        Internet/FTPServer
)

# HTTP Server
add_library(HTTPSERVER_FILES STATIC)

target_sources(HTTPSERVER_FILES PUBLIC
        Internet/httpServer/httpParser.c
        Internet/httpServer/httpServer.c
        Internet/httpServer/httpUtil.c
)

target_include_directories(HTTPSERVER_FILES PUBLIC
        Ethernet
        Internet/httpServer
)

# MQTT
add_library(MQTT_FILES STATIC)

target_sources(MQTT_FILES PUBLIC
        Internet/MQTT/mqtt_interface.c
        Internet/MQTT/MQTTClient.c
        Internet/MQTT/MQTTPacket/src/MQTTConnectClient.c
        Internet/MQTT/MQTTPacket/src/MQTTConnectServer.c
        Internet/MQTT/MQTTPacket/src/MQTTDeserializePublish.c
        Internet/MQTT/MQTTPacket/src/MQTTFormat.c
        Internet/MQTT/MQTTPacket/src/MQTTPacket.c
        Internet/MQTT/MQTTPacket/src/MQTTSerializePublish.c
        Internet/MQTT/MQTTPacket/src/MQTTSubscribeClient.c
        Internet/MQTT/MQTTPacket/src/MQTTSubscribeServer.c
        Internet/MQTT/MQTTPacket/src/MQTTUnsubscribeClient.c
        Internet/MQTT/MQTTPacket/src/MQTTUnsubscribeServer.c
)

target_include_directories(MQTT_FILES PUBLIC
        Ethernet
        Internet/MQTT
        Internet/MQTTPacket/src
)

# SNTP
add_library(SNTP_FILES STATIC)

target_sources(SNTP_FILES PUBLIC
        Internet/SNTP/sntp.c
)

target_include_directories(SNTP_FILES PUBLIC
        Ethernet
        Internet/SNTP
)

# TFTP
add_library(TFTP_FILES STATIC)
target_sources(TFTP_FILES PUBLIC
        Internet/TFTP/netutil.c
        Internet/TFTP/tftp.c
)
target_include_directories(TFTP_FILES INTERFACE
        Internet
        Internet/TFTP
)
target_link_libraries(TFTP_FILES PRIVATE
        ETHERNET_FILES
        pico_stdlib
)

# multicast
add_library(MULTI_FILES STATIC)

target_sources(MULTI_FILES PUBLIC
        Application/multicast/multicast.c
)

target_include_directories(MULTI_FILES PUBLIC
        Ethernet
        Application/multicast
)
