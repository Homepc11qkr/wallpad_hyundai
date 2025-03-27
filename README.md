# wallpad_hyundai
# https://github.com/eigger/espcomponents/tree/master/packages/wallpad/hyundai


현대 월패드 구성 
ttl to 485 wallpad connection  
github 정보 > external_components >
485 연결에 현대통신 월패드 스위치 보일러 센서 구성입니다
    
# https://cafe.naver.com/homestation/222
 
# https://github.com/eigger/espcomponents/tree/master/packages/wallpad
 
# https://github.com/Homepc11qkr/wallpad_hyundai

    external_components:
      - source: github://eigger/espcomponents/relreases/latest
        components: [ uartex ]
        refresh: always

external_components:
  # - source: github://eigger/espcomponents/relreases/latest
  - source: github://eigger/espcomponents@v250312
    # 2025_0327_2358_01
    components: [ uartex ]
    refresh: always  
    

전체 esphome esp32 basic 제품과 ttl to 485 구성  yaml 파일은
s:\esphome\485_ttl_esp32dev_ip84.yaml
파일을 참조 바랍니다.

업데이트 > 2025_0308_0136_05 

> s:\esphome\ttlto485_esp32_s3_m16_ip85.yaml

https://cafe.naver.com/homestation/237

https://11q.kr/www/bbs/board.php?bo_table=co3&wr_id=2823

업데이트 정보 > 27-03-25 23:58 42
S:\esphome\ttlto485_esp32_s3_m16_ip85.yaml
상태패킷추가

interval:
  - id: interval_update
    interval: 5000ms  # 초기값 (5초)
    then:
      - if:
          condition:
            switch.is_on: interval_uart_sw
          then:
            - delay: 1s
            - uartex.write:
                data: [0x0B, 0x01, 0x18, 0x01, 0x46, 0x11, 0x00, 0x00]
            - delay: 1s
            - uartex.write:
                data: [0x0B, 0x01, 0x18, 0x01, 0x46, 0x12, 0x00, 0x00]
            - delay: 1s
            - uartex.write:
                data: [0x0B, 0x01, 0x18, 0x01, 0x46, 0x13, 0x00, 0x00]
            - delay: 1s
            - uartex.write:
                data: [0x0B, 0x01, 0x18, 0x01, 0x46, 0x14, 0x00, 0x00]
            - delay: 1s
            - uartex.write:
                data: [0x0B, 0x01, 0x19, 0x01, 0x40, 0x11, 0x00, 0x00]
            - delay: 1s
            - uartex.write:
                data: [0x0B, 0x01, 0x19, 0x01, 0x40, 0x12, 0x00, 0x00]
            - delay: 1s
            - uartex.write:
                data: [0x0B, 0x01, 0x19, 0x01, 0x40, 0x13, 0x00, 0x00]
            - delay: 1s
            - uartex.write:
                data: [0x0B, 0x01, 0x19, 0x01, 0x40, 0x14, 0x00, 0x00]
            - delay: 1s
            - uartex.write:
                data: [0x0B, 0x01, 0x19, 0x01, 0x40, 0x15, 0x00, 0x00]

switch:
  - platform: gpio
    name: "interval_uart_sw_5_Sec"
    id: interval_uart_sw
    pin: GPIO12  # 사용할 핀 번호 (필요에 따라 수정)
    inverted: false  # 핀의 반전 여부, 필요에 따라 조정
    restore_mode: ALWAYS_ON  # ESP32가 재부팅 후에도 기본적으로 켜져 있도록 설정
    on_turn_on:
      - lambda: |-
          ESP_LOGD("interval_uart_sw", "Switch turned on.");
    on_turn_off:
      - lambda: |-
          ESP_LOGD("interval_uart_sw", "Switch turned off.");
=============> 월패드 없이 스위치 동작시 esphome 바로 동작 > 2025_0328_0002_05

