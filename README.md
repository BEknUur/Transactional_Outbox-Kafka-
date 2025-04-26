📦 Order Service — Transactional Outbox + Kafka
Этот проект демонстрирует реализацию паттерна Transactional Outbox с использованием Spring Boot, Kafka и PostgreSQL.
События сохраняются в базу данных вместе с бизнес-операцией и позже отправляются в Kafka.

🚀 Как запустить проект
1. Клонируй репозиторий
git clone https://github.com/your-username/order-outbox-service.git
cd order-outbox-service
2. Запусти инфраструктуру через Docker
docker-compose up -d
Будут запущены:

PostgreSQL (5432)
Kafka (9092)
Zookeeper
Kafka UI (8085)
3. Настрой application.properties
Убедись, что файл src/main/resources/application.properties содержит:

spring.kafka.bootstrap-servers=localhost:9092

spring.datasource.url=jdbc:postgresql://localhost:5432/outbox_db
spring.datasource.username=your_user
spring.datasource.password=your_password

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
4. Запусти Spring Boot приложение
./mvnw spring-boot:run
🔗 Swagger UI
Документация доступна по адресу:
http://localhost:8080/swagger-ui.html

🔁 Пример API запроса
POST /api/orders

{
  "product": "Wireless Mouse",
  "quantity": 1,
  "price": 49.99,
  "customerEmail": "test@user.com"
}
⚙️ Как работает Transactional Outbox
Заказ сохраняется в таблицу orders
Событие сохраняется в outbox_events в той же транзакции
Планировщик OutboxScheduler каждые 5 сек. отправляет событие в Kafka
После успешной отправки событие помечается как published=true
🧪 Проверка событий
Перейди на http://localhost:8085
Открой топик orders.order_created в Kafka UI и проверь сообщение

🧰 Технологии
Java 21
Spring Boot 3
Spring Data JPA
PostgreSQL
Apache Kafka
Docker & Docker Compose
Spring Kafka
Swagger UI
Lombok