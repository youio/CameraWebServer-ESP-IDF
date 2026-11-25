idf_component_register(SRCS "myCamServer.c" "app_httpd.cpp" "wifi_utils.c"
                    INCLUDE_DIRS "."
                    PRIV_REQUIRES esp_wifi esp_http_server nvs_flash esp_psram esp_timer esp_event esp_netif)
