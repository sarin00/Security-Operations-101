## 1. План заняття
На минулому занятті ми познайомились з вже розгорнутим Elastic SIEM, і розслідували інцидент з логів які вже були у наявності в цій SIEM. В реальності, вам рано чи пізно доведеться самостійно розгорнути SIEM систему, налаштувати її, додати альорти для підозрілих подій, встановити агенти SIEM на операційні системи, і тільки потім вже росзлідувати інциденти. Саме цим ми сьогодні і займемось.  
### 1.1 Дії
1. Створити акаунт на Elastic і [запустити тріальну версію їх SaaS рішення](https://www.elastic.co/cloud/cloud-trial-overview) (банківська картка не потрібна для цього)
2. Підняти Windows машинку яка буде "жертвою атаки". Це імітація звичайних робочих станцій нашої компанії які ми маємо захищчати
3. Включити інтеграцію Elastic Defend. Integrations -> Elastic Defend -> кнопка "Add Elastic Defend" -> Додати до Agent Policy -> створити нову Agent Policy.
4. Встановити на Windows elastic agent. Будьте обережними з тим в яку папку ви завантажите агент та з якої папки будете його запускати. В інсталяційному гайді вам надасться кілька команд які треба виконати на Windows машині у PowerShell. Ці команди окремі, не одне ціле, і запускаються по черзі.
5. Перейти в Analytics -> Discover, і перевірити що логи з Windows OS надсилаються у Elastic. За замовчуванням логи відправляються кожну хвилину.
6. Включити заготовані правила детектування від Elastic для EDR. Security -> Rules -> Detection Rules -> Tags -> OS:Windows, виділити всі повернені результати -> Bulk actions -> Enable.
7. Відкрийте правило "Suspicious PowerShell Execution" та подивіться на те, на яку сае активність це правило буде сваритись.
8. Додати інтеграцію "Windows" до ранішествореного Agent Group
9. Запустити імітатори шкідливого софту на Windows, що змусить Elastic створити альорти  
    [APT simulator](https://github.com/NextronSystems/APTSimulator)  
    [Ransomware simulator](https://www.knowbe4.com/free-cybersecurity-tools/ransomware-simulator)  
    [Powershell ransomware simulator](https://github.com/JoelGMSec/PSRansom)
    [Powershell reverse shell](https://swisskyrepo.github.io/InternalAllTheThings/cheatsheets/shell-reverse-cheatsheet/#powershell)  
    [Code execution](https://www.ired.team/offensive-security/code-execution)
10. Розслідувати альорти в Elastic, зрозуміти які події трапились на Windows OS, хто став причиною зараження, і т.д.
