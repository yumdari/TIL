```c
void flash_erase_page(uint16_t page_no) {

    // max page no == 2047
    if (page_no > AT45DB041X_MAX_PAGE_NO) return;

    SPI_Select();
    SPI_Tx(0x81); //page erase
    SPI_Tx((uint8_t) (page_no >> 8) & 0x07); //5 dummy + 3 address bits
    SPI_Tx((uint8_t) (page_no) & 0xFF); //8 address bits
    SPI_Tx(0x00); //8 dummy bits
    SPI_Deselect();

    //wait erase
    flash_wait_ready();
}
```

flash_erase_page 함수는 page_no 에 해당하는 페이지의 데이터를 삭제하는 함수 입니다.

데이터시트를 보면 256바이트의 페이지를 사용하는 경우, 0x81 커맨드 이후에 5비트 dummy + 11비트 address + 8비트 dummy 를 전송하도록 가이드 하고 있습니다.