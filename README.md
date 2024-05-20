go_service - test task for genesis school
---
Service can show USD currency rate and allow to subscribe to updates by mail.
What is not realised:
- Mail sending updates: instead, there is stub adapter, that inform about intent to send a message.
- Docker compose run flow: there are some problems with running built golang application

Some rules from Clean Architecture was used in the development: The main idea is divide service into layers like entities, use cases, adapters and infrastructure layers. But, due to the small size of the service, it was decided to combine some layers. Now, presentation layer, that contains http endpoints and mailer task, also have a business logic from use cases layer, but layers still independent for each other because they denepd on abstractions, that described in common package. Thus the Dependency Inversion Principle is fulfilled.  
Endpoints receive own dependencies by Dependency Injection by go closures.

What can be improved?
---
- Mailing task can be rewritten by special task queues like Celery, because we need to control task status, restart on failure and etc.
- Choose another web framework. Service has simple two endpoints, so, net/http was used. Another framework can be more effective in this case or if we need to complicate a service
- add tests
- setup CI/CD, like GitHub Actions
