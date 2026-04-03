# CST8915 Lab 8: Algonquin Pet Store on Steroids

**Student Name**: Anoop Sidhu
**Student ID**: 040984994
**Course**: CST8915 Full-stack Cloud-native Development
**Semester**: Winter 2026

---
## Demo Video

🎥 [Watch Demo Video](https://youtu.be/tv4NRhJ_J_Q)

---
## Technical Explanation of Task 2

- Using Kubernetes PersistentVolumeClaims to add persistence to Mongo.
- Volume mounted on `/data/db`
- Increased mongodb replicas to 3 for increased durability.
- Added storage block, which persists even if pod is deleted.
- Verified by querying for the same `ObjectId` between deployments.
- Used same pattern on RabbitMQ, persisting `/var/lib/rabbitmq`, unfortunately could not achieve persistence.

---
## Potential MongoDB and RabbitMQ replacements

- RabbitMQ: **Azure Service Bus** - managed azure message queue service. Offers competitive pricing. Also easier to scale than RabbitMQ, and can integrate with existing JMS applications.
- MongoDB: **Azure DocumentDB** - managed azure database with open-source, MongoDB-compatible engine. Instant automatic scaling and high availability (depending on subscription).