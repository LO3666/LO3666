#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

#define SCREEN_WIDTH 128  // OLED顯示屏的寬度
#define SCREEN_HEIGHT 64  // OLED顯示屏的高度

// 宣告OLED的I2C地址
#define OLED_RESET    -1  // 4-Pin OLED通常不使用這個引腳
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

void setup() {
  // 初始化Serial通訊
  Serial.begin(115200);

  // 初始化OLED顯示屏
  if (!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) {  // 預設I2C地址是0x3C
    Serial.println(F("OLED初始化失敗"));
    for (;;);  // 如果初始化失敗，則進入死循環
  }

  // 清除緩存
  display.clearDisplay();

  // 設置顯示亮度 (默認是100，值的範圍是0-255)
  display.dim(0);  // 0 表示全亮，1 表示微亮

  // 設置字體大小、顏色
  display.setTextSize(1);      // 字體大小
  display.setTextColor(SSD1306_WHITE);  // 字體顏色

  // 設置文字顯示位置 (左上角)
  display.setCursor(0, 0);

  // 顯示文字
  display.println(F("Hello, OLED!"));

  // 更新顯示
  display.display();

  // 等待2秒
  delay(2000);

  // 繪製一個簡單的圖形
  display.clearDisplay();
  display.drawCircle(SCREEN_WIDTH / 2, SCREEN_HEIGHT / 2, 20, SSD1306_WHITE);
  display.display();
}

void loop() {
  // 可以在這裡添加更新顯示的其他程式碼
}
