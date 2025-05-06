Code used for sensor:

#include "mcc_generated_files/system/system.h"

#define AHT21_ADDR 0x38
#define MY_ID 'E'  // This subsystem's ID

void send_uart_message(const char* msg) {
    for (uint8_t i = 0; i < 8; i++) {
        while (!EUSART1_IsTxReady());
        EUSART1_Write(msg[i]);
    }
}

void send_temp_to(char receiver, uint8_t temp) {
    char msg[8] = {
        'F', 'S',
        MY_ID, receiver,        // Sender = 'E', Receiver = 'T' or 'K'
        (temp / 10) + '0',      // Tens digit
        (temp % 10) + '0',      // Ones digit
        'F', 'S'                // Footer
    };
    send_uart_message(msg);
}

void read_and_send_temp(void) {
    uint8_t cmd[3] = {0xAC, 0x33, 0x00};
    uint8_t data[6];

    I2C1_Write(AHT21_ADDR, cmd, 3);
    __delay_ms(80);

    if (I2C1_Read(AHT21_ADDR, data, 6) && !(data[0] & 0x80)) {
        uint32_t raw_temp = ((uint32_t)(data[3] & 0x0F) << 16) | ((uint32_t)data[4] << 8) | data[5];
        float temperature = ((float)raw_temp / 1048576.0f) * 200.0f - 50.0f;
        uint8_t temp_int = (uint8_t)temperature;

        send_temp_to('T', temp_int);  // Send to Sanjith
        __delay_ms(10);
        send_temp_to('K', temp_int);  // Send to Kevin
    }
}

int main(void)
{
    SYSTEM_Initialize();
    INTERRUPT_GlobalInterruptEnable();
    INTERRUPT_PeripheralInterruptEnable();

    char rx_buf[8] = {0};

    while (1)
    {
        // === UART Message Handling ===
        if (EUSART1_IsRxReady()) {
            char byte = EUSART1_Read();

            for (uint8_t i = 0; i < 7; i++) rx_buf[i] = rx_buf[i + 1];
            rx_buf[7] = byte;

            if (rx_buf[0] == 'F' && rx_buf[1] == 'S' &&
                rx_buf[6] == 'F' && rx_buf[7] == 'S') {

                char sender   = rx_buf[2];
                char receiver = rx_buf[3];

                if (receiver == MY_ID) {
                    // This message is for us ? trigger temp reading
                    read_and_send_temp();
                } else {
                    // Not for us ? forward
                    send_uart_message(rx_buf);
                }
            }
        }
    }
}
