## 1. Вступ
### 1.1 Різниця між інцидентом та подією
Інструменти типу SIEM генерують десятки альортів та логують сотні тисяч записів на день. Різниця між подією та інцидентом критична, бо ці дві речі мають різні рівні пріорітету.  
`Подія, або альорт` - це повідомлення, які вимагають розслідування людиною. Вони можуть бути False Positive (хибне спрацювання, коли активність виявилась легітимною), чи True Positive (активність виявилась і справді шкідливою і альорт переходить у статус інциденту).  
`Інцидент` - це підтверджена шкідлива/небажана активність, які вимагає повноцінної реакції на інцидент.  

### 1.2 Абревіатури та сленг
`IR` - Incident Response  
`CIRT (CSIRT)` - Computer Incident Response Team (Cyber Security Incident Response Team)  
`SOC` - Security Operations Center  
`Alert (альорт)` - автоматизоване повідомлення про активність, яка вимагає розслідування. Альорти можуть бути як створені вендорами інстурментів, так і створені вручну аналітиками для пошуку активності яка їх цікавить. Зазвичай ми створюємо альорти шляхом визначення подій чи активностей, які для нас є підозрілими. Ці події мають в якомусь вигляді логуватись та/чи моніторитись, щоб наші інструменти могли автоматично їх задетектувати. Наприклад, наша SIEM система збирає всі логи з компʼютерів з ОС Windows. Ми створюємо альорт для кожного запуску процесу powershell.exe коли parent process є explorer.exe, бо хочемо детектувати кожен раз коли користувач компʼютера запускає powershell.exe. Коли людина запустить powershell, наша SIEM створить альорт і повідомить нас про це.  
`False Positive` - "хибно позитивне" спрацювання, коли створився альорт на легітимну, нормальну активність. Наприклад, альорт про запуск powershell.exe від explorer.exe, коли при розслідуванні виявилось що системний адміністратор запускав powershell щоб перевірити деякі налаштування OS. Це легітимна активність, і альорт закривається як False Positive.  
`True Positive` - альорт, який при розслідуванні виявився шкідливою/небажаною активністю/кібератакою. Такий альорт переходить у статус інциденту.  

### 1.3 Як працює Security Analyst (аналітик з кібербезпеки)
Коли ми говоримо про Incident Response, аналітики працюють так само як і детективи в серіалах. Ми збираємо до купи всю інформацію яка має цінність та відношення до події, ми складаємо пазли у загальну картину про те, що саме сталось і в якому порядку. Ми покладаємось виключно на факти, безсумнівні докази (хеші, IP адреси, доменні імена, цифрові підписи, сигнатури, тощо), а також дуже багато гуглимо.  
Попри мислення як детективи, ми також маємо мислити як зловмисники. Які способи проникнення у нашу мережу ми бачимо, які сліпі зони чи непропатчені, забуті системи ми маємо, які дані нашої компанії є найкритичнішими для нас, які вірогідні цілі для атаки матимуть хакери, тощо.  

### 1.4 Проблеми, які вже вирішіли за вас
Ти не перший і не останній кібербезпечник, якому треба вибудувати IR екосистему у своїй компанії. Замість того щоб вигадувати колесо, варто спиратись на загальноприйняті стандарти, чи фреймворки. Наприклад:  
1. [NIST SP 800-61 Computer Security Incident Handling Guide](https://csrc.nist.gov/pubs/sp/800/61/r2/final)
2. [NIST SP 800-86 Guide to Integrating Forensic Techniques into Incident Response](https://csrc.nist.gov/pubs/sp/800/86/final)

## 2. Incident Response Phases (Етапи Розслідування Інцидентів)
Рослідування інцидентів - це великий і вмісткий процес який складаєтсья з різних етапів, і якість підготовки та виконання цих етапів визначить наскільки ефективно ви зможете детектувати, розслідувати, та зупиняти кібератаки у своїй компанії.  

Є кілька версій цих фаз від різних джерел, але всі вони мають приблизно однакову суть:  
1. Preparation (Підготовка)  
2. Detection and Analysis (Детектування та розслідування події)  
3. Containment (Ізоляція інфекції та зупинення її поширення по мережі)  
4. Eradication (Знищення інфекції, що важче ніж здається)  
5. Recovery (Відновлення нормальної роботи бізнесу)  
6. Lessons learned (Активності після інциденту та покращення IR процесів)

### 2.1 Preparation (Підготовка до інцидентів)
На відміну від всіх нуступних етапів, підготовка це постійні активності, покращення, планування, та навчання, які робляться до інциденту. Це найважливіший етап, бо без нього навіть найкращі аналітики не дадуть гарного результату в росзлідуванні інцидентів.  

Коли станеться інцидент, які інструменти це задетектують, або як саме працівники компанії повідомлять тебе про підозрілу активність? Як саме ти розслідуватимеш цю подію, кому ти повідомиш про інцидент та хто з твоєї компанії буде частиною CSIRT команди? Які інструменти для кожного з етапів IR ти маєш використовувати? Який у вас план дій по відновленню нормальної роботи бізнесу? Чи є у вас бекапи, де вони, та як саме відновитись з цих бекапів? Що робити, якщо вся корпоративна мережа комунікації перестане працювати, чи ти знаєш номери телефонів членів CSIRT? Якщо корпоративні компʼютері стануть недоступними, які компʼютери використовуватимуть аналітики, як ці компʼютери отримають доступ до корпоративної мережі? Таким питанням нема кінця, але відповідати на них - це і є ціль фази підготовки до IR, і саме через це ця фаза постійна і ніколи не закінчується.  

