Provide your solution here:

Diagram
+--------------------------------------------------+
| Web (Cloudfront)                                |
+--------------------------------------------------+
| Routing (Route53)                               |
+--------------------------------------------------+
| Load Balancer (AWS ALB)                         |
+--------------------------------------------------+
| API Layer (AWS API Gateway, AWS Lambda)         |
+--------------------------------------------------+
| Load Balancer (AWS NLB)                         |
+--------------------------------------------------+
| Service (EKS + ElastiCache + DynamoDB)          |
+--------------------------------------------------+
| Event Streaming (Amazon MKS)                    |
+--------------------------------------------------+
| Database (Aurora PostgreSQL)                    |
+--------------------------------------------------+
| Monitoring & Logging (CloudWatch, Amazon Managed Service for Prometheus)   |
+--------------------------------------------------+



Role and Alternative:
Cloudfront:
  Role: Accelerate access to web application.
  Alternative: We can use other CDN solution like Cloudflare, Akamai ... CloudFront integrates seamlessly with other AWS services for security (with AWS Shield and AWS WAF) and performance.
Route53:
  Role: Manage DNS routing, supports advanced routing policies—for example, latency-based or geolocation routing—and performs health checks to redirect traffic away from failed endpoints
  Alternative: Other DNS solutions like Cloudflare ... but Route53 offers simplicity and deep integration with AWS’s ecosystem.
AWS ALB:
  Role: Handles handles incoming HTTPS requests by performing SSL termination, host/path-based routing, and basic traffic filtering.
  Alternative: AWS NLB could be used for ultra-low latency proxying, but ALB provides richer features for web and API traffic.
AWS API Gateway:
  Role: Fronts a serverless API, optimized for high-concurrent requests.
  Alternative: Containerizing the API on EKS is possible. However API Gateway provides native scaling and pay-per-use cost benefits.
AWS NLB:
  Role: Handles internal traffic flows between the API layer and backend microservices in EKS.
  Alternative: AWS ALB might be sufficient for some workloads but NLB is optimized for extreme performance at the transport layer (TCP/UDP) with very low latency.
EKS:
  Role: Hosts containerized microservices. Deploying across multiple availability zones ensures resilience
  Alternative: Running services on EC2 instances without orchestration is a possibility; however, EKS provides modern orchestration with built-in resilience and easier scaling.
ElastiCache:
  Role: Real-time caching and transient data that demands sub-millisecond access times.
  Alternative: Containerizing the Redis on EKS is possible. However ElastiCache reduces operational complexity and ensures on-demand scaling without manual intervention.
DynamoDB:
  Role: Serves as a highly performant NoSQL database for non-relational, high-velocity data
  Alternative: DocumentDB could have been selected but DynamoDB’s native scalability, fully managed nature, and integration with AWS Lambda make it a compelling choice for dynamic workloads.  
Amazon MKS:
  Role: Event streaming and message queuing. AWS native service that provides a managed Apache Kafka solution.
  Alternative: Containerizing the Kafka on EKS is possible however with Amazon MSK, you can use Kafka without needing to manage the underlying infrastructure or worry about the operations of your Kafka clusters.
Aurora PostgreSQL:
  Role: Primary relational database for storing crucial transactional data, including order histories, account balances, and ledger entries.It delivers high performance through its built-in replication, auto-scaling read replicas, and multi-AZ deployment which ensures fault tolerance and data integrity.
  Alternative: While NoSQL options address certain use cases and were chosen for part of the service layer, Aurora ensures that complex relational queries and ACID transactions are handled reliably—an essential requirement in financial systems.
CloudWatch:
  Role: Aggregates logs, captures metrics from AWS services, and sends alerts for performance or operational anomalies throughout the platform.
  Alternative: While third-party monitoring tools exist. CloudWatch is a monitoring service designed specifically for AWS resources and cost-effectiveness for AWS users.
Amazon Managed Service for Prometheus:
  Role: Collects detailed metrics from the containerized microservices. These metrics feed into auto-scaling decisions and provide deep insights into the health and performance of the system.
  Alternative: Containerizing the Prometheus on EKS is possible but Amazon Managed Service for Prometheus is a fully managed service, reduces operational load and ensures seamless integration with AWS services.



Scaling Strategy
API and Lambda: automatically scale based on traffic.
EKS: Auto scaling supports adding more pods when service demand grows.
DynamoDB: Auto-scaled throughput ensures that increasing write/read loads are handled without manual intervention
Aurora PostgreSQL: Read replicas and clustering support scaling for intensive analytical queries, while write scaling is managed by Aurora’s inherent optimizations.
