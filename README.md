# ⚖️ Distributed Load Balancer & Health Monitor

## 📌 Project Overview
This project is a custom-engineered Layer 7 (Application) Load Balancer simulation built natively in Python. It demonstrates core principles of distributed systems engineering, dynamic traffic routing, and automated fault tolerance without relying on external web frameworks. 

## 🛠️ Core Engineering Mechanics

* **Dynamic Routing Algorithms:** Engineered to support multiple traffic distribution strategies. The default implementation utilizes a **Least Connections** algorithm, intelligently routing incoming packets to the backend node with the lowest active thread count, preventing bottlenecks.
* **Fault Tolerance & Health Checking:** Deployed an asynchronous background daemon thread that actively monitors the heartbeat of all backend servers. If a node suffers a hardware failure (simulated randomly), the load balancer instantly removes it from the healthy pool, ensuring zero dropped user requests.
* **Concurrency Control:** Utilized `threading.Lock()` mechanics across the Server and Router classes to prevent race conditions during high-frequency concurrent traffic spikes, ensuring accurate connection tracking and metric aggregation.
* **Graceful Degradation:** Handles catastrophic failure states dynamically. If all backend nodes crash simultaneously, the router safely degrades, returning simulated `503 Service Unavailable` errors rather than crashing the primary execution thread.

## 🚀 Execution
The application executes a multithreaded simulation (`client_traffic`) spawning 25 asynchronous requests. During execution, the health daemon randomly forces nodes offline and brings them back online. The terminal output provides a real-time trace of how the routing algorithm adapts to the changing network topology, concluding with an aggregated traffic distribution report.
