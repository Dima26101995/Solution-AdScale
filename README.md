# Solution-AdScale

Проектная работа 2 курса **«Архитектор решений»**.
Кейс: **AdScale** — SaaS-платформа цифровой рекламы (RTB), интеграция с крупной DSP-площадкой.

## Контекст

Монолит (C++/Go/Python/Node) на одной PostgreSQL, без кеша, очередей и контейнеризации.
**15 000 RPS** в пике, **P95 110–120 мс** при требовании ≤100 мс. После интеграции с DSP —
**18 000 RPS** (через 3 мес), **50 000 RPS** (через год), SLA партнёра **≤80 мс**.

## Структура

```
Task1/   Архитектурная диагностика и целевое видение
         README.md · as-is.md · drivers.md · TO-BE.md · diagrams/ · adr/
Task2/   Проектирование RTB и интеграция с DSP
         README.md · bidding-service.md · interaction.md · api-gateway.md · reliability.md · diagrams/
Task3/   Данные, масштабирование и отказоустойчивость
         README.md · database-strategy.md · scaling.md · caching.md · event-streaming.md · failover.md · diagrams/
```

## Ключевые решения

- **Стратегия эволюции:** Strangler Fig — постепенное вырезание сервисов из монолита, критический путь первым
  (**API Gateway** → **Bidding** → **Statistics** → Analytics → Financial → остальное). Непрерывность бизнеса сохраняется.
- **Сервисы:** Bidding · Campaign · Delivery · Statistics · Analytics · Financial · Dashboard BFF · API Gateway.
- **Инфраструктура:** Kafka-кластер (события), Redis (кеш), PostgreSQL per service, ClickHouse (аналитика),
  Kubernetes, наблюдаемость (Prometheus/Grafana, OpenTelemetry/Jaeger, ELK).
- **Взаимодействие:** DSP → Gateway → Bidding (HTTP/OpenRTB); Bidding ↔ Campaign
  (REST через ACL на этапе 1, gRPC на этапе 2);
  события — Kafka (доставка не менее одного раза, DLQ, идемпотентный потребитель);
  финансы — асинхронно + идемпотентность + сверка.
- **Время отклика:** бюджет времени по шагам, без синхронной БД на критическом пути, Circuit Breaker + fallback.

## Формат сдачи

Markdown; диаграммы — PlantUML (предпочтительно) / Structorizr / Draw.io; ADR — стандартный формат.
Публичный репозиторий + пул-реквест.

## Статус

- [x] Task 1
- [x] Task 2
- [x] Task 3
