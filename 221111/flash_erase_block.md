```c
void flash_erase_block(uint8_t block_no) {

    uint16_t page_no = (block_no << 3); //8 page = 1 block    

    SPI_Select();
    SPI_Tx(0x50); //block erase
    SPI_Tx((uint8_t) (page_no >> 8) & 0x07); //5 dummy + 3 address bits
    SPI_Tx((uint8_t) (page_no) & 0xFF); //8 address bits
    SPI_Tx(0x00); //8 dummy bits
    SPI_Deselect();

    //wait erase
```

flash_erase_block 은 블록 단위로 데이터를 삭제하는 함수입니다.

8개의 페이지가 모이면 1개의 블록이 되기 때문에 block_no 을 3번 Left Shift 하면 삭제하고자 하는 블록의 시작 페이지의 11비트 주소값을 얻을 수 있습니다.

해당 페이지 주소값을 0x50 커맨드와 함께 전송하면 블록 단위로 데이터가 삭제됩니다.

flash_erase_all 함수는 flash_erase_block 함수를 반복 호출하여 전체 256개 블록을 모두 삭제합니다.