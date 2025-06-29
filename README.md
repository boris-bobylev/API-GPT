# Примеры работы с API

## Пример 1: Работа с API OpenAI (ChatGPT)

```python
import requests

# Замените на свой ключ API OpenAI
api_key = "your_openai_api_key_here"
prompt = "Придумай 5 идей для мобильного приложения"

# Отправляем запрос в API OpenAI
response = requests.post(
    "https://api.openai.com/v1/chat/completions",
    headers={
        "Authorization": f"Bearer {api_key}",
        "Content-Type": "application/json"
    },
    json={
        "model": "gpt-3.5-turbo",  # Модель GPT-3.5, также можно использовать GPT-4
        "messages": [{"role": "user", "content": prompt}],
        "temperature": 0.7,  # Степень случайности ответа
        "max_tokens": 2000  # Максимальное количество токенов в ответе
    }
)

# Проверяем успешность запроса
if response.status_code == 200:
    print(response.json()["choices"][0]["message"]["content"])
else:
    print("Ошибка:", response.status_code, response.text)
```

**Описание:**
Этот пример показывает, как использовать API OpenAI для генерации идей с использованием модели GPT-3.5. В запросе передается текстовый запрос, и возвращается текст с предложениями.

---

## Пример 2: Работа с API DeepSeek

```python
import requests

# Замените на свой ключ API DeepSeek
api_key = "your_deepseek_api_key_here"
prompt = "Придумай 5 идей для мобильного приложения"

# Отправляем запрос в API DeepSeek
response = requests.post(
    "https://api.deepseek.com/v1/chat/completions",
    headers={
        "Authorization": f"Bearer {api_key}",
        "Content-Type": "application/json"
    },
    json={
        "model": "deepseek-chat",  # Указываем модель для DeepSeek
        "messages": [{"role": "user", "content": prompt}],
        "temperature": 0.7,  # Степень случайности ответа
        "max_tokens": 2000  # Максимальное количество токенов в ответе
    }
)

# Проверяем успешность запроса
if response.ok:
    print(response.json()["choices"][0]["message"]["content"])
else:
    print("Ошибка:", response.status_code, response.text)
```

**Описание:**
В этом примере показано, как использовать API DeepSeek для генерации текстовых ответов. Запрос передается через `POST` с указанием ключа и параметров.

---

## Пример 3: Работа с API Qwen

```python
import requests

# Замените на свой ключ API Qwen
api_key = "your_api_key_here"
prompt = "Придумай 5 идей для мобильного приложения"

# Отправляем запрос в API Qwen
response = requests.post(
    "https://dashscope.aliyuncs.com/api/v1/services/aigc/text-generation/generation",  # URL API
    headers={
        "Authorization": f"Bearer {api_key}",
        "Content-Type": "application/json"
    },
    json={
        "model": "qwen-turbo",  # Указываем модель Qwen
        "input": {"messages": [{"role": "user", "content": prompt}]},
        "parameters": {
            "temperature": 0.7,
            "max_tokens": 2000
        }
    }
)

# Проверяем успешность запроса
if response.status_code == 200:
    result = response.json()
    print(result["output"]["choices"][0]["message"]["content"])
else:
    print("Ошибка:", response.status_code, response.text)
```

**Описание:**
Здесь мы отправляем запрос в API Qwen для генерации текстовых идей. Используем модель `qwen-turbo` и получаем ответ, выводя его на экран.

---

## Пример 4: Работа с API GigaChat

```python
from gigachat import GigaChat
from gigachat.models import Chat, Messages, MessagesRole

# Авторизация через сертификат или логин/пароль
# Вариант 1: С использованием токена (полученного заранее)
giga = GigaChat(credentials='your_auth_token_here', verify_ssl_certs=False)

# Вариант 2: С использованием логина и пароля (если нет токена)
# giga = GigaChat(credentials="your_login:your_password", verify_ssl_certs=False)

prompt = "Придумай 5 идей для мобильного приложения"

# Формируем запрос
messages = [Messages(role=MessagesRole.USER, content=prompt)]

# Отправляем запрос и получаем ответ
response = giga.chat(Chat(messages=messages, temperature=0.7, max_tokens=2000))

# Выводим ответ
print(response.choices[0].message.content)
```

**Описание:**
Этот пример демонстрирует, как использовать библиотеку GigaChat для общения с моделью. Мы создаем запрос и получаем ответ через метод `chat`.

---

## Общие рекомендации:
1. Всегда проверяйте статус ответа от API, чтобы убедиться, что запрос прошел успешно.
2. Настройте параметры запроса в зависимости от нужд, такие как `temperature` (случайность) и `max_tokens` (длина ответа).
3. Используйте библиотеки `requests` для удобной работы с HTTP-запросами.
