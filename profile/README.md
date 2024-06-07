# Paidify

SOA-based distributed online payment system. Intended for generic educational institutions transactions.

<img src="https://github.com/Paidify/.github/assets/73978713/12b3ed54-82d3-4433-84e9-3bddb9ffdbfc">

## Getting Started

Although Paidify should ideally be mounted in distributed servers accross a network, here is a guide to run it locally.

This process is guided by the [`run-local`](https://github.com/Paidify/run-local) app. It will start 11 terminals, one for each [service](https://github.com/Paidify#architecture) instance.

### Requirements

- [Node.js](https://nodejs.org).
- [Docker](https://www.docker.com) along with [Docker Compose](https://docs.docker.com/compose/).

### Steps

1. Clone `run-local` repository.

       git clone https://github.com/Paidify/run-local.git

2. Install dependencies and start the application.

       npm install && npm start

3. Follow the steps shown in the application.

<img src="https://github.com/Paidify/.github/assets/73978713/0d963496-3220-42e3-b94e-5486bac9910c">

You will press enter to confirm launching each terminal. It is recommended to leave a reasonable amount of time between each service, so that your PC can run them properly.

## Architecture

<img src="https://github.com/Paidify/.github/assets/73978713/4995b563-2058-4ed6-9946-e11d4e6a65dc">

- **[Bank Database](https://github.com/Paidify/db-bank.git)**: Representation of both East Bank and Western Bank databases. *MongoDB with Docker*.
- **[East Bank API](https://github.com/Paidify/BankEastRepo.git)**: Representation of API provided by East Bank. *Node.js*.
- **[Western Bank API (same code as East Bank API)](https://github.com/Paidify/BankEastRepo.git)**: Representation of API provided by Western Bank. *Node.js*.
- **[Paidify DB and University DB](https://github.com/Paidify/db-paidify.git)**: Paidify central database, including University database schema. *MySQL with Docker*.
- **[Monitor DB](https://github.com/Paidify/db-monitor.git)**: Database for monitoring service instances. Used for Circuit Breaker pattern. *MySQL with Docker*.
- **[Gateway](https://github.com/Paidify/api-gateway.git)**: API Gateway to handle incoming request from client application. *Node.js*.
- **[Authentication Service](https://github.com/Paidify/authentication-service.git)**: Service for user authentication. *Node.js*.
- **[Queries Service](https://github.com/Paidify/queries-service.git)**: Service for handling general queries from client application. *Node.js*.
- **[Payment Service](https://github.com/Paidify/Payment-Gateway.git)**: Service for handling payment transactions. *Node.js*.
- **[Card Balance Service](https://github.com/Paidify/balance-gateway.git)**: Service for handling card balance queries. *Node.js*.
- **[Client application](https://github.com/Paidify/paidify-web.git)**: Client application for Paidify. *Next.js*.

## Data Models

### Paidify Schema

<img src="https://github.com/Paidify/.github/assets/73978713/b2e2496f-7b65-43e6-9352-f49d8ddf61d6">

### Generic University Schema

<img src="https://github.com/Paidify/.github/assets/73978713/59b01739-2cfb-4af7-8491-5abbb862f0e7">

### Bank Database Schema (approximation by ChatGPT)

```text
+----------------+       +----------------+       +---------------+
| Owner          |       | CardFranchise  |       | CardType      |
|----------------|       |----------------|       |---------------|
| owner_id (PK)  |       | franchise_id(PK)|       | type_id (PK)  |
| name           |       | franchise       |       | type          |
| email          |       +----------------+       +---------------+
| DNI            |
+----------------+
        |
        |
+-------v--------+       +---------------+  
| Card           |       | Deal          |  
|----------------|       |---------------|  
| card_id (PK)   |       | deal_id (PK)  |  
| owner_id (FK)  |       | ref_number(UQ)|  
| exp_month      |       | successful     | 
| exp_year       |       | eff_date       | 
| cvv            |       | amount         | 
| franchise_id(FK)|       | balance        |
| type_id (FK)   |       | dues_number    | 
| amount         |       | fulfilled      | 
| card_number(UQ)|       +---------------+  
+----------------+                          
```

## Views

### Home

<img src="https://github.com/Paidify/.github/assets/73978713/c7efc9c1-1ca8-442f-a5f8-895fdb24210a">

### Payment methods

<img src="https://github.com/Paidify/.github/assets/73978713/99824bff-90a1-448a-a40f-3470ccd9bdf5">

### Payments

<img src="https://github.com/Paidify/.github/assets/73978713/727fed69-90f4-4026-bc67-02c311b16eb6" width="700">

<img src="https://github.com/Paidify/.github/assets/73978713/ed80a77d-ef87-4047-9fb9-4a5cfa41d9d1" width="700">

<img src="https://github.com/Paidify/.github/assets/73978713/f87d797b-42bf-45a1-a7d7-c7b7f688b088" width="700">

<img src="https://github.com/Paidify/.github/assets/73978713/2352e62f-d16b-4956-95b0-520d49c0b2ee" width="700">

If Nodemailer is set up in Payment Gateway, an email will be sent to the desired email address.

### History

<img src="https://github.com/Paidify/.github/assets/73978713/89c0b7e2-38a5-4704-8942-122e67ef1e7b" width="700">
<img src="https://github.com/Paidify/.github/assets/73978713/96c02d00-eae0-4abd-a6a6-8fccc80220be" width="700">

## Built with

- [Node.js](https://nodejs.org).
- [Docker](https://www.docker.com).
- [Next.js](https://nextjs.org).
- [MySQL](https://www.mysql.com).
- [MongoDB](https://www.mongodb.com).
- [ExpressJS](https://expressjs.com/es/).
- [Nodemailer](https://nodemailer.com).
