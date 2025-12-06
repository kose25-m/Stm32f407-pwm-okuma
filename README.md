# STM32F407 PWM Okuma ile  Motor Kontrolü

STM32F407 tabanlı bu projede, PA0 ve PA2 pinlerinden gelen PWM sinyallerinin görev döngüsü (duty cycle) TIM2 input capture ile okunur ve bu değerler TIM3 üzerinden 4 motorun ileri/geri yön ve fren kontrolünde kullanılır. 
Kodda yer alan `adjust_input_duty()` fonksiyonu, benim kullandığım motor sürücüsünün orta konumu ve tolerans aralığını yazılımsal olarak filtrelemek için eklenmiştir.
bu sayede sürücünün ölü bölgesi dengelenir. Farklı bir sürücü kullanıyorsanız veya böyle bir tolerans problemi yoksa, bu fonksiyonu kullanmak zorunda değilsiniz.
isterseniz tamamen kaldırabilir veya kendi sisteminize göre yeniden düzenleyebilirsiniz.

It is an STM32F407-based example that reads the duty cycle of PWM signals on PA0 and PA2 using TIM2 input capture and uses these values to control motors (forward/reverse and brake) via TIM3 PWM outputs. 
The `adjust_input_duty()` function is added to compensate the tolerance and deadband of the motor driver I use by filtering the input duty value in software, so the driver’s non-linear behavior around the center is smoothed out.
If your motor driver does not have this kind of tolerance issue, you do not have to use this function; you can remove it completely or adapt it to match your own driver characteristics.
---

## Özellikler / Features

Bu proje, iki PWM girişinden okunan duty cycle değerlerini kullanarak motorları ileri/geri yön ve fren kontrolü ile sürmeyi amaçlayan örnek bir STM32F407 uygulamasıdır. 
Timer ve pin ayarları STM32CubeIDE üzerinden kolayca farklı kartlara veya sürücülere uyarlanabilir.

This project is an STM32F407 example that uses duty cycle values from two PWM inputs to drive four DC motors with forward/reverse and brake control.
Timer and pin settings can be easily adapted to other boards or drivers via STM32CubeIDE.

---

## Donanım / Hardware

Bu örnek, STM32F4 serisi bir kart (örneğin STM32F407 Discovery) üzerinde test edilmiştir. İki PWM giriş kanalı, dört motor PWM çıkışı ve yön/fren pinleri kullanılmaktadır.
Kendi projenizde farklı pinler veya sürücüler kullanıyorsanız, sadece CubeIDE içerisindeki pin ve timer konfigürasyonunu değiştirmeniz yeterlidir.

This example has been tested on an STM32F4 series board (e.g. STM32F407 Discovery). It uses two PWM input channels, four motor PWM outputs, and direction/brake GPIOs. 
If you use different pins or drivers in your own project, you only need to update the pin and timer configuration in CubeIDE.

---

## Geliştirme Ortamı / Development Environment

Proje, STM32CubeIDE ve HAL kütüphaneleri kullanılarak C dilinde geliştirilmiştir.
Kod yapısı, CubeMX tarafından üretilen iskelet üzerinde `/* USER CODE BEGIN */` blokları içerisine eklenen kullanıcı kodları ile ilerlemektedir.

The project is developed in C using STM32CubeIDE and the HAL libraries.
The code is based on the CubeMX-generated skeleton, with user code added inside the `/* USER CODE BEGIN */` blocks.

---

## Kullanım / Usage

Bu projeyi kendi kartınızda denemek için:
1. Projeyi STM32CubeIDE ile açın.
2. Gerekirse clock, pin ve timer ayarlarını kartınıza göre güncelleyin.
3. PWM giriş kaynaklarınızı (RC alıcı, başka MCU vb.) PA0 ve PA2 pinlerine bağlayın ve GND’yi ortaklayın.
4. Motor sürücülerinizi TIM3 PWM çıkışlarına ve yön/fren pinlerine bağlayın.
5. Projeyi derleyip karta yükleyin; `printf` çıktıları veya debugdan live expression üzerinden değişken isimlerini yazıp üzerinden okunan duty değerlerini ve motor davranışını izleyebilirsiniz.

To try this project on your own board:
1. Open the project in STM32CubeIDE.
2. Update the clock, pin and timer settings according to your hardware if needed.
3. Connect your PWM sources (RC receiver, another MCU, etc.) to PA0 and PA2 and share the same GND.
4. Connect your motor drivers to the TIM3 PWM outputs and direction/brake pins.
5. Compile the project and upload it to the card; you can write the variable names via `printf` outputs or live expression from debug and watch the duty cycle values ​​and engine behavior.

---

## Notlar / Notes

Bu repo, gömülü yazılım ve motor kontrolü ile ilgilidir paylaşılmıştır. Kendi projenizde:
- Farklı motor sürücüleri,
- Farklı PWM frekansları,
- Farklı yön/fren mantıkları

kullanabilirsiniz; kod yapısı bu tür değişikliklere göre kolayca uyarlanabilecek şekilde düzenlenmiştir.

This repository is shared as a starting example for those interested in embedded software and motor control. In your own project you may use:
- Different motor drivers,
- Different PWM frequencies,
- Different direction/brake logic,

and adapt the code structure accordingly.
