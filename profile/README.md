![image alt](https://github.com/ARGENIX-Embedded/Argenix-MIK32-Amur-Project/blob/main/Repository%20content/Logo.png?raw=true)

## Описание

**( 🛠 В разработке )** Открытая программно-аппаратная экосистема для разработки электронных устройств на базе ограниченной линейки микроконтроллеров архитектуры RISC-V, предоставляющая фирменные отладочные платы для комфортной разработки. 

Экосистема предлагает лаконичный синтаксис, максимальную эффективность и безопасность по сравнению с традиционными HAL на чистом Си, благодаря современному инструментарию языка программирования Zig. Проект основывается на пакетах драйверов собственной разработки **ARIS (Argenix RISC-V Interface Standard)**. Благодаря этому один и тот же код, написанный на Аргеникс, будет запускаться на разных чипах — достаточно просто сменить пакет драйверов.

## Бенчмарк

| Платформа  | Чип                       | Прошивка          | Занимаемая ПЗУ | Занимаемая ОЗУ |
| :---:      | :---:                     | :---:             | :---:          | :---:          |
| АРГЕНИКС   | МИК32 (К1948ВК015)        | Led Blink         | 72 Байт        | 0 Байт         |
| Arduino    | ATmega328P                | Led Blink         | 924 Байт       | 9 Байт         |
| STM32 Cube | STM32F103C8T6 (Blue Pill) | Led Blink         | 1240 Байт      | 34 Байт        |

## Пример Blink
```zig
const Core = @import("../aris/core/Core.zig");
const BaseLibs = @import("../base_libraries/BaseLibs.zig");

const PIN_0_0 = BaseLibs.PinLib.PIN_0_0;
const SysTimer = Core.SysTimer;

export fn main() void {
    SysTimer.init();
    PIN_0_0.setMode(.OUTPUT);

    while (true) {
        PIN_0_0.setState(.HIGH);
        SysTimer.delayMs(300);
        PIN_0_0.setState(.LOW);
        SysTimer.delayMs(300);
    }
}
```
```text
Вес прошивки ПЗУ: 72 байт, ОЗУ: 0 байт
```

## Лицензия
Проект распространяется под лицензией [Apache 2.0](LICENSE).
