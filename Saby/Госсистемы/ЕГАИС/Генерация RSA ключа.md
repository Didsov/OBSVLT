### Генерация RSA ключа
1. Получить RSA нужно на каждую точку продаж
2. Для этого откройте домашнюю страницу УТМ localhost:8080/home/ ( сборка должна быть не нижу 2600
3. Перейдите в раздел Сервисы/Генерация ключа
4. Указать роль. (ЮР или Физлицо. Для физ лица нужна [[Saby/Госсистемы/ЕГАИС/МЧД]])
5. Выберите подразделение на получения ключа
6. Примите условия и сгенерируйте ключ
7. После завершите работу УТМ
8. В директории УТМ\transporter нужно переименовать transportDB и xml
9. Запустите УТМ снова
10. Откройте файл C:\UTM\transporter\conf\transport.properties и укажите ПИН-коды носителя.