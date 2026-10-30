# Task 3 — Данные, масштабирование и отказоустойчивость

## Задача

Обеспечить работу с данными при росте **18 000 → 50 000 RPS**: своё хранилище у каждого
сервиса, стратегия масштабирования, кэширование, потоковая обработка событий
и восстановление после отказов.

## Состав

| Файл | Содержание |
|---|---|
| [`database-strategy.md`](database-strategy.md) | База для каждого сервиса, обоснование выбора |
| [`scaling.md`](scaling.md) | Репликация master-slave, read replicas, CQRS, шардирование, автоскейлинг |
| [`caching.md`](caching.md) | Что кэшируем, Redis, TTL, инвалидация, прогрев |
| [`event-streaming.md`](event-streaming.md) | Топики Kafka, схемы, группы, retention, DLQ |
| [`failover.md`](failover.md) | RPO/RTO, бэкапы, сценарии отказов, 12-factor |
| [`diagrams/`](diagrams/) | Топология данных, масштабирование, поток событий |

## Диаграммы

| Диаграмма | Файл | Что показывает |
|---|---|---|
| C4 Container | `diagrams/database-topology.puml` | Сервис → хранилище, владение данными |
| C4 Container | `diagrams/scaling-topology.puml` | Репликация, read replicas, CQRS |
| C4 Container | `diagrams/event-streaming.puml` | Топики Kafka, продюсеры и потребители |

## Целевые показатели

| Показатель | Значение |
|---|---|
| RPO финансов | 0 |
| RTO финансов | 15 минут |
| RPO кампаний | 5 минут |
| RTO кампаний | 30 минут |
| Потеря событий | 0 (replay из Kafka) |
| Доступность (год) | SLA 99.9% |
