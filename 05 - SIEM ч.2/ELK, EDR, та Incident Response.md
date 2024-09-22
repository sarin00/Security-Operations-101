## 1. План заняття
На минулому занятті ми познайомились з вже розгорнутим Elastic SIEM, і розслідували інцидент з логів які вже були у наявності в цій SIEM. В реальності, вам рано чи пізно доведеться самостійно розгорнути SIEM систему, налаштувати її, додати альорти для підозрілих подій, встановити агенти SIEM на операційні системи, і тільки потім вже росзлідувати інциденти. Саме цим ми сьогодні і займемось.  
### 1.1 Дії
1. Створити акаунт на Elastic і запустити тріальну версію їх SaaS рішення (банківська картка не потрібна для цього)
2. Підняти Windows машинку яка буде "жертвою атаки". Це імітація звичайних робочих станцій нашої компанії які ми маємо захищчати
3. Встановити на Windows elastic agent
4. Додати до Elastic фічу Endpoint Security, налаштувати її для групи в якій знаходиться Windows жертва
5. Включити заготовані правила детектування від Elastic для EDR
6. Запустити імітатори шкідливого софту на Windows, що змусить Elastic створити альорти  
    [APT simulator](https://github.com/NextronSystems/APTSimulator)  
    [Ransomware simulator](https://www.knowbe4.com/free-cybersecurity-tools/ransomware-simulator)  
    [Powershell ransomware simulator](https://github.com/JoelGMSec/PSRansom)
    [Powershell reverse shell](https://swisskyrepo.github.io/InternalAllTheThings/cheatsheets/shell-reverse-cheatsheet/#powershell)  
    [Code execution](https://www.ired.team/offensive-security/code-execution)
7. Розслідувати альорти в Elastic, зрозуміти які події трапились на Windows OS, хто став причиною зараження, і т.д.
