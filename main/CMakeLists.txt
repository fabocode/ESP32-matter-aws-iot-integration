set(
    PRIV_REQUIRES_LIST 
        device 
        esp_matter 
        esp_matter_console 
        app_reset 
        protocol_examples_common
    )

set(
    MQTT_SRCS 
        "mqtt_demo_mutual_auth.c" 
        "app_main.cpp"
        "app_driver.cpp"
        "../components/common/posix_compat/clock_esp.c"
    )

set(
    POSIX_INCLUDE_DIRS 
        ../components/common/posix_compat
    )

set(
    REQUIRES
        coreMQTT
        backoffAlgorithm
    )

idf_component_register(
    SRCS  
        "mqtt_demo_mutual_auth.c"
        "app_main.cpp"
        "app_driver.cpp"
    SRC_DIRS  
        "." 
    INCLUDE_DIRS  
        ${POSIX_INCLUDE_DIRS}
    PRIV_INCLUDE_DIRS  
        "."           
    PRIV_REQUIRES  
        ${PRIV_REQUIRES_LIST}
    REQUIRES  
        ${REQUIRES}
    )

set_property(
    TARGET 
        ${COMPONENT_LIB} 
    PROPERTY 
        CXX_STANDARD 14
    )
target_compile_options(
    ${COMPONENT_LIB} 
    PRIVATE 
    "-DCHIP_HAVE_CONFIG_H"
    )
