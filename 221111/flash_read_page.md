flash_read_page 함수는 page_no 에 해당하는 페이지에서 len 길이만큼 데이터를 읽어서 buffer 에 반환하는 기능을 수행합니다.

데이터시트에 따르면, 0xD2 커맨드 뒤에 이어서 5비트의 dummy, 11비트의 page 주소, 8비트의 page 내 시작 주소를 전달 후, 4바이트의 dummy 데이터를 전송해 주어야 합니다.

```c
void flash_read_page(uint16_t page_no, uint8_t *buffer, size_t len) {

    // max page no = 2047 & max buffer size = 256
    if (page_no > AT45DB041X_MAX_PAGE_NO || len > AT45DB041X_PAGE_SIZE) return;

    SPI_Select();
    SPI_Tx(0xD2); //read main memory page
    SPI_Tx((uint8_t) (page_no >> 8) & 0x07); //5 dummy + 3 address bits
    SPI_Tx((uint8_t) (page_no) & 0xFF); //8 address bits
    SPI_Tx(0x00); //start address within page

    SPI_Tx(0x00); //4 dummy bytes to read
    SPI_Tx(0x00);
    SPI_Tx(0x00);
    SPI_Tx(0x00);

    while (len > 0) {
        *buffer++ = SPI_Rx();
        len--;
    }
    SPI_Deselect();
}
```