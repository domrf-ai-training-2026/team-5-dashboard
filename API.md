# Контракт API — команда 5

GET https://domrf-ai-training-2026.github.io/team-5-dashboard/data.json

Все данные вымышлены. Публичный read-only JSON, без ключа. CORS не требуется между проектами одной организации, поскольку их origin одинаков: https://domrf-ai-training-2026.github.io. Для форков на другом origin проверьте CORS в браузере. Не используйте режим no-cors: он не даёт читать JSON.

## Общий формат

schema_version: строка 1.0; team_id: число 5; synthetic: true; updated_at: ISO UTC; units: единицы; records: массив записей. Ключ строки: task_id.

- period — Неделя до
- office_id — Код офиса
- office — Офис
- city — Город
- task_id — ID поручения (идентификатор)
- subject — Поручение
- owner_role — Ответственный
- deadline — Срок (YYYY-MM-DD)
- status — Статус (статус)
- priority — Приоритет

Статусы зафиксированы на конец указанной недели. Не сравнивайте deadline с сегодняшней датой. Выполнение = выполненные / все поручения. task_id уникален.

## Пример чтения

```js
const response = await fetch(API_URL, {cache: 'no-store'});
if (!response.ok) throw new Error('HTTP ' + response.status);
const payload = await response.json();
if (payload.schema_version !== '1.0' || !Array.isArray(payload.records))
  throw new Error('Неверный формат API');
```

Держите видимыми источник, updated_at и время успешного чтения. При ошибке не подменяйте результат нулями и не оставляйте старые цифры без отметки. Публикация коммита и распространение кэша Pages занимают время; проверяйте успешный deploy и updated_at.

## Принимаемый источник

Команда 1: https://domrf-ai-training-2026.github.io/team-1-dashboard/data.json

Добавьте выполнение плана из API команды 1, чтобы сопоставить результаты офиса и исполнение поручений.
