# Task 2 — Проектирование RTB и интеграции с DSP

## Задача

Спроектировать сервис ставок и интеграцию с новой DSP-площадкой: **18 000 RPS**,
P95 **не более 100 мс** (для DSP — **80 мс**), без деградации текущих клиентов.
Исходно: монолит на 15 000 RPS с P95 110–120 мс, без кеша и очередей, срок — 3 месяца.

## Состав

| Файл | Содержание |
|---|---|
| [`bidding-service.md`](bidding-service.md) | Границы, API, зависимости, модель данных, НФТ |
| [`interaction.md`](interaction.md) | Протоколы, паттерны взаимодействия, топики Kafka, выбор Gateway |
| [`api-gateway.md`](api-gateway.md) | Маршрутизация, лимиты, аутентификация, Circuit Breaker, мониторинг |
| [`reliability.md`](reliability.md) | Circuit Breaker, повторы, идемпотентность, резервные стратегии |
| [`diagrams/`](diagrams/) | Компонентная и sequence-диаграммы |

## Диаграммы

| Диаграмма | Файл | Что показывает |
|---|---|---|
| C4 Component | `diagrams/component-bidding-service.puml` | Устройство Bidding Service |
| Sequence | `diagrams/sequence-bid-request.puml` | Обработка `bid-request` |
| Sequence | `diagrams/sequence-failover.puml` | Сценарии деградации |

## Целевые показатели

| Показатель | Значение |
|---|---|
| Пропускная способность | 18 000 RPS |
| P95 времени отклика | ≤100 мс (DSP ≤80 мс) |
| Доступность Bidding Service | Без сбоев; деградация до no-bid |
| Масштабирование | Горизонтальное, stateless |
