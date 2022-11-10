### 1. Program - 쓰기 동작

### " Floating Gate에 전자를 charge시켜 Vth를 증가시키는 동작 "

1. Floating gate와 control gate에 강한 양전압 인가 & Source, Drain, p-substrate 접지
2. 강한 전계에 의해 에너지 밴드가 휘어짐에 따라 p형 기판의 전자가 충분한 에너지를 얻어 FN Tunneling에 의해 tunneling oxide 층을 통과해 floating gate에 저장됨
3. Floating gate 내 전자들이 수직방향 전계를 방해하여 Vth가 증가함

※ FN Tunneling : 산화막의 에너지 밴드 banding에 의해 전자가 얇아진 장벽을 통과하는 현상

---

### 2. Erase - 지우기 동작

### " Floating Gate에 있는 전자를 빼내어 Vth를 감소시키는 동작 "

데이터를 저장하기 위해서는 floating gate 내에 전자가 채워져 있으면 제대로 데이터를 기록할 수 없기 때문에 erase 동작을 통해 전자를 제거해야 한다.

1. p형 기판에 강한 양전압 인가 & Control gate 접지 & Source, Drain Floating
2. 강한 전계에 의해 floating gate 내 전자들이 tunneling oxide를 통과해 p형 기판으로 빠져나옴
3. Floating gate에 전자가 없어 수직방향 전계가 효과적으로 전달되므로 Vth가 감소함

※ NAND Flash는 블록을 지우기 전에 새로운 데이터를 쓸 수 없기 때문에 쓰기시간지연이 있다. (쓸 데이터가 0인지 1인지 모르는 상태에서 전자가 FG 내에 남아 있으면 데이터를 제대로 기록할 수 없음)

---

### 3. Read - 읽기 동작

### " Floating Gate 내 전자 유무에 따른 Vth 값의 차이로 데이터를 읽음 "

1. 읽을 소자에 PROGRAM/ERASE 중간 수준에 해당하는 읽기 전압을 인가 & 나머지 소자는 Vth 이상의 전압을 인가
2. BL에 전류가 흐르는지의 여부에 따라 데이터를 읽음
- FG 내 전자 존재 o (Program 상태) → Vth 증가 → 전류 흐르지 않음 (OFF) → "0" 인식
- FG 내 전자 존재 x (Erase 상태) → Vth 감소 → 전류 흐름 (ON) → "1" 인식

![https://k.kakaocdn.net/dn/caFXZ7/btruQkikB0n/dWzwyngNyuCFTUxoOMZ3D1/img.png](https://k.kakaocdn.net/dn/caFXZ7/btruQkikB0n/dWzwyngNyuCFTUxoOMZ3D1/img.png)

전달특성곡선