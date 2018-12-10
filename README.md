# I2C AVR

I2C Master device implementation for ATmega (328P) controllers without using Interrupts. 

## Getting Started

Copy both i2c_master.h and i2c_master.c to your project and just start using it. 

### Example of usage

At the begining of programm call the initialization routine by using the following method:

```C
i2c_master_init(I2C_SCL_FREQUENCY_100);
```

This function accepts unsigned long as frequency. You can use predefined `I2C_SCL_FREQUENCY_100` for 100 kHz and `I2C_SCL_FREQUENCY_400` for 400kHz.

For sending bytes use one of the following methods after performing the initialization:

```C
uint8_t i2c_master_sendByte(uint8_t address, uint8_t data);
uint8_t i2c_master_send(uint8_t address, uint8_t* data, uint16_t length);
```

For receiving data use the following method:
```C
uint8_t i2c_master_receive(uint8_t address, uint8_t* data, uint16_t length);
```

Both methods accepts addresses of device without shifting (pass the address without shifting on 1 and applied READ/WRITE bit)

### Error handling
Methods for sending and receiving data can return error codes if anything was not correct. In case of success method returns 0 (predefined `I2C_STATUS_SUCCESS`), otherwise - one of the following error codes:

- `I2C_STATUS_ERROR_START_WAS_NOT_ACCEPTED` = 10
- `I2C_STATUS_ERROR_TRANSMIT_OR_READ_WAS_NOT_ACKNOWLEDGED` = 20
- `I2C_STATUS_ERROR_TRANSMIT_NOT_ACKNOWLEDGED` = 21
- `I2C_STATUS_ERROR_READ_NOT_ACKNOWLEDGED` = 22

Current library contains function for retrieving textual description of error by its code:
```C
const char* i2c_getErrorMessage(uint8_t errorCode);
```

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
