# AWS Lambda Interview Questions

## Basic AWS Lambda Interview Questions

1. **What is AWS Lambda?**
   - **Answer**: AWS Lambda is a serverless compute service that lets you run code without provisioning or managing servers. You pay only for the compute time you consume, and it automatically scales your applications by running code in response to events.

2. **What are the benefits of using AWS Lambda?**
   - **Answer**:
     - **No Server Management**: No need to provision or manage servers.
     - **Pay Only for What You Use**: Charged based on the number of requests and compute time.
     - **Automatic Scaling**: Scales automatically based on the number of incoming requests.
     - **High Availability**: Built-in fault tolerance and high availability.
     - **Supports Multiple Languages**: Supports Node.js, Python, Ruby, Java, Go, .NET Core, and more.

3. **What is an AWS Lambda function?**
   - **Answer**: A Lambda function is the code you upload to AWS Lambda. It is triggered in response to events such as HTTP requests, changes to data in an S3 bucket or DynamoDB table, or custom events.

4. **How do you trigger an AWS Lambda function?**
   - **Answer**: AWS Lambda functions can be triggered by various AWS services, including:
     - **API Gateway**: For HTTP requests.
     - **S3**: For changes to an S3 bucket (e.g., object upload).
     - **DynamoDB**: For table updates.
     - **SNS/SQS**: For message notifications.
     - **CloudWatch Events/Logs**: For scheduled events or log processing.

5. **What is a Lambda execution role?**
   - **Answer**: A **Lambda execution role** is an IAM role that grants the Lambda function permission to access AWS services and resources (e.g., read/write to S3, DynamoDB). It defines what the function is allowed to do.

## Intermediate AWS Lambda Interview Questions

6. **What is the maximum execution time of a Lambda function?**
   - **Answer**: The maximum execution time (timeout) for a Lambda function is **15 minutes**.

7. **What are Lambda Layers, and why would you use them?**
   - **Answer**: **Lambda Layers** are a way to manage common code, libraries, or dependencies that you want to use across multiple Lambda functions. They help reduce deployment package size and simplify code management.

8. **What is AWS Lambda cold start?**
   - **Answer**: A **cold start** occurs when a Lambda function is invoked for the first time or after a period of inactivity. AWS Lambda needs to provision a new instance, which adds a delay (latency) before the function begins execution.

9. **How can you reduce AWS Lambda cold start times?**
   - **Answer**:
   - **Provisioned Concurrency**: Keeps a certain number of instances ready to handle requests.
   - **Minimize Package Size**: Reduce the size of the deployment package.
   - **Use Smaller Memory Settings**: Smaller functions have shorter initialization times.
   - **Use VPC Wisely**: Avoid unnecessary VPC configurations that can slow down cold starts.

10. **What are AWS Lambda environment variables?**
    - **Answer**: **Environment variables** are key-value pairs that can be used to store configuration settings, database connection strings, or other information needed by your Lambda function at runtime.

## Advanced AWS Lambda Interview Questions

11. **Explain the Lambda invocation types: Synchronous vs. Asynchronous.**
    - **Answer**:
      - **Synchronous Invocation**: The caller waits for the function to process the event and return a response. Example: API Gateway invoking Lambda.
      - **Asynchronous Invocation**: The caller sends the event to Lambda and immediately moves on. Lambda processes the event in the background. Example: S3 event triggers.

12. **What is Lambda Provisioned Concurrency, and how does it work?**
    - **Answer**: **Provisioned Concurrency** is a feature that keeps a specified number of Lambda instances initialized and ready to handle requests. This eliminates cold start latency and is useful for performance-sensitive applications.

13. **How do you monitor AWS Lambda functions?**
    - **Answer**: AWS Lambda monitoring can be done through:
      - **CloudWatch Metrics**: Provides metrics like invocations, duration, errors, and throttles.
      - **CloudWatch Logs**: Captures the function's output logs.
      - **X-Ray**: Provides end-to-end tracing to analyze performance and troubleshoot issues.

14. **How can you secure AWS Lambda functions?**
    - **Answer**:
    - Use **IAM Roles** with the least privilege.
    - **Encrypt environment variables**.
    - **VPC Integration** for secure access to resources.
    - **Enable VPC Flow Logs** and **AWS CloudTrail** for auditing.

15. **How can Lambda integrate with VPC, and what are the implications?**
    - **Answer**: Lambda can be configured to access resources in a VPC, such as RDS or EC2 instances. When integrated with a VPC, Lambda functions may experience increased cold start times due to the need to set up ENIs (Elastic Network Interfaces).

# AWS API Gateway Interview Questions

## Basic API Gateway Interview Questions

1. **What is Amazon API Gateway?**
   - **Answer**: Amazon API Gateway is a fully managed service that allows developers to create, publish, maintain, monitor, and secure RESTful and WebSocket APIs at any scale.

2. **What are the key features of API Gateway?**
   - **Answer**:
     - **Request and Response Transformation**: Modify API requests and responses.
     - **Rate Limiting and Throttling**: Control the number of API calls to prevent abuse.
     - **Caching**: Reduce latency and load by caching API responses.
     - **Security**: Integration with AWS IAM, Cognito, and Lambda authorizers for security.
     - **Monitoring and Metrics**: Integration with CloudWatch for monitoring.

3. **What are the types of APIs supported by API Gateway?**
   - **Answer**:
     - **REST APIs**: Traditional HTTP APIs for web services.
     - **WebSocket APIs**: For real-time two-way communication.
     - **HTTP APIs**: Simplified RESTful APIs with lower cost and improved performance.

4. **How does API Gateway integrate with AWS Lambda?**
   - **Answer**: API Gateway can be configured to trigger Lambda functions in response to HTTP requests. API Gateway takes care of request/response transformation, authentication, and authorization before forwarding the request to Lambda.

5. **What is a usage plan in API Gateway?**
   - **Answer**: A **usage plan** in API Gateway allows you to set throttling limits and quotas for individual API keys, helping you manage and monitor access to your API.

## Intermediate API Gateway Interview Questions

6. **What is the difference between REST API and HTTP API in API Gateway?**
   - **Answer**:
     - **REST API**: Feature-rich, supports advanced features like request/response validation, caching, WAF integration, and more. It is suitable for complex use cases.
     - **HTTP API**: Simplified, cost-effective, and provides lower latency. Ideal for microservices, HTTP backends, and mobile/web applications needing simple API functionalities.

7. **How do you secure APIs created with API Gateway?**
   - **Answer**:
     - Use **API Keys** for client identification.
     - Use **IAM Roles and Policies** to restrict access.
     - Implement **Lambda Authorizers** or **Cognito User Pools** for custom authorization.
     - Enable **AWS WAF** to protect against common web exploits.
     - Use **SSL/TLS** encryption for secure communication.

8. **What are custom domain names in API Gateway?**
   - **Answer**: **Custom domain names** allow you to use your domain name (e.g., `api.yourdomain.com`) for your API instead of the default API Gateway domain. You can configure custom domains with AWS Certificate Manager (ACM) for SSL certificates.

9. **What is request and response mapping in API Gateway?**
   - **Answer**: **Request and response mapping** templates allow you to modify or transform the request payload sent to your backend service or the response payload returned by the backend. This is useful for adapting the input/output format of your backend with the client's expected format.

10. **How does API Gateway handle CORS (Cross-Origin Resource Sharing)?**
    - **Answer**: API Gateway allows you to configure **CORS** settings to specify which origins are allowed to access your API. You can enable CORS on specific methods to control which HTTP methods (GET, POST, etc.) and headers are allowed.

## Advanced API Gateway Interview Questions

11. **What is the purpose of stages in API Gateway?**
    - **Answer**: **Stages** in API Gateway represent different versions or environments of an API (e.g., development, staging, production). They allow you to deploy different versions of your API and manage configurations like logging, caching, and throttling independently.

12. **How does API Gateway caching work, and why is it useful?**
    - **Answer**: API Gateway provides caching at the **stage level** to store responses for a specified time-to-live (TTL) period. Caching reduces the number of requests made to the backend, decreases latency, and improves performance and cost-effectiveness.

13. **What is an API Gateway Lambda Authorizer?**
    - **Answer**: An **API Gateway Lambda Authorizer** (formerly known as a custom authorizer) is a Lambda function that is invoked by API Gateway to control access to your API. It uses token-based authentication (like JWT tokens) and allows you to implement custom authorization logic.

14. **Explain throttling and rate limiting in API Gateway.**
    - **Answer**:
      - **Throttling**: Limits the steady-state rate of requests and bursts to protect backend services from being overwhelmed.
      - **Rate Limiting**: Controls the number of requests a client can make within a specific period. Can be defined at the API stage or usage plan level.

15. **How can you deploy changes in API Gateway?**
    - **Answer**:
      - Make changes to your API in the **API Gateway console** or using AWS CLI/SDKs.
      - Deploy these changes to a specific **stage** (e.g., dev, prod).
      - Use **stage variables** to manage different configurations and environments.

16. **How can you monitor and troubleshoot API Gateway APIs?**
    - **Answer**:
      - **CloudWatch Metrics**: Monitor API performance, request count, latency, and errors.
      - **CloudWatch Logs**: Enable logging to capture request and response data, and identify issues.
      - **X-Ray**: Use AWS X-Ray for end-to-end tracing and debugging of API requests.

17. **What is API Gateway Edge-Optimized vs. Regional vs. Private API?**
    - **Answer**:
      - **Edge-Optimized APIs**: Designed for clients globally and routes requests through the AWS CloudFront edge locations.
      - **Regional APIs**: Targets clients in the same AWS region, offering lower latency for region-specific applications.
      - **Private APIs**: Accessible only within a VPC using VPC endpoints, ideal for internal applications.

18. **Explain API Gateway's integration types.**
    - **Answer**:
      - **HTTP/HTTP_PROXY Integration**: Directly forwards requests to an HTTP endpoint.
      - **Lambda Proxy Integration**: Invokes a Lambda function, passing the full request data.
      - **Mock Integration**: Used for testing without a backend; returns a response directly from API Gateway.
      - **AWS Service Integration**: Enables invoking other AWS services (like S3, SNS, DynamoDB) directly from API Gateway.
