flash_write_page 함수는 buffer 에 담겨있는 len 길이의 데이터를 page_no 에 해당하는 페이지에 기록하는 작업을 수행합니다.

erase_first 옵션을 사용하는 경우에는 별도 page erase 를 먼저 수행하지 않고도 writing 동작을 수행할 수 있습니다.

쓰기 동작은 버퍼쓰기 + Page 쓰기 2단계로 수행됩니다. 우선 0x84 커맨드를 이용해서 쓰고자 하는 데이터를 버퍼에 우선 적재하여 줍니다. 적재가 완료되면 0x83 또는 0x88 커맨드를 이용해서 원하는 페이지에 버퍼에 담겨있는 데이터를 저장합니다.

```c
void flash_write_page(uint16_t page_no, uint8_t *buffer, size_t len, uint8_t erase_first) {

    // max page no = 2047 & max buffer size = 256
    if (page_no > AT45DB041X_MAX_PAGE_NO || len > AT45DB041X_PAGE_SIZE) return;

    SPI_Select();
    SPI_Tx(0x84); //buffer1 write command
    SPI_Tx(0x00); //8 dummy bit
    SPI_Tx(0x00); //8 dummy bit
    SPI_Tx(0x00); //8 buffer address

    while (len > 0) {
        SPI_Tx(*buffer++); //write to buffer
        len--;
    }
    SPI_Deselect();

    SPI_Select();
    if (erase_first) {
        SPI_Tx(0x83); //write buffer1 to page with built-in erase
    } else {
        SPI_Tx(0x88); //write buffer1 to page without built-in erase
    }
    SPI_Tx((uint8_t) (page_no >> 8) & 0x07); //5 dummy + 3 address bits
    SPI_Tx((uint8_t) (page_no) & 0xFF); //8 address bits
    SPI_Tx(0x00); //8 dummy bits
    SPI_Deselect();

    flash_wait_ready();
```