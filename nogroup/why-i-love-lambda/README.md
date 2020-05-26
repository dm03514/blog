# Why I Love AWS Lambda (and think serverless is the future)

Since February I've been working on an asynchronous AWS Lambda service processing 60,000 events / second from Kinesis. Lambda provides minimal operational overhead, fast deploys, predictable pricing, and enforces many tenants of 12-factor apps, out of thee box. After working with Lambda almost daily for the past 3 months, I’m convinced it’s the future for asynchronous processing, and here’s why.

# Outsourcing 

Lambda removes complexity over stateful deployment models. This minimizes the surface area service engineers are responsible for. Lambda removes the need for system alerts, instance sizing, autoscaling, provisioning servers, and choosing process monitors, amongst others. There's no SSH’ing into instances since Lambda manages them. Lambda removes the amount a company needs to manage and reason about. In VM or container based deployments service teams are responsible for keeping services up and running 24x7 365. With Lambda, scheduling and execution becomes Amazon's responsibility. A companies responsibility is minimized to ensure that their Lambda functions work correctly, and can keep up with throughput, and costs are bound. 

There’s an opportunity cost with keeping processes running. Time spent on instance maintenance and process upkeep is time *not* spent on other work. Although I don't have any concrete metrics on the break down of time in a serverless vs non-serverless systems, but I would have expected to SSH into a system some amount of times in the last 3 months, especially for a system of this level of throughput. Other sources of time saved are: 

- provisioning servers
- reproducing environments locally
- monitoring processes
    
All of these result in time saved when using Lambda. Anecdotally, I feel like I’ve saved 10-15% of time in just not having to manage servers, concurrency, scaling, alerting, OS upgrades, integrations, etc. 

# Reliability 

Amazon is better at running distributed systems than most of the the industry. They devote a huge amount of resources and budget to ensuring they are. Lambda minimizes the surface area of components that can fail. It would be naive to think that Amazon doesn’t go down because it does, but there are just less moving parts on a Lambda consumer's end. Lambda shifts the operational complexity to Amazon, who’s core competency is to execute Lambdas reliably. Additionally, Amazon has more resources to mobilize when there are customer facing issues. 

Outsourcing infrastructure to Amazon also changes the dynamic of the issues that customers encounter. Instead of servers, processes and scaling, it shifts issues to a higher level -- closer to the business domain. Lambda shifts the failure domain up a level of abstraction to one that is closer to the business and the consumer's domain.

# Predictable Pricing

The service I work with is cheaper to run on Lambda than EC2. Lambda is especially good for bursty traffic since it can idle down to 0 resources. Even if it’s not cheaper in all cases, Lambda is more predictable and simple. Lambda billing is based on the number of invocations and the duration of each invocation. Measure how long the Lambda takes on average, and multiple that by the projected throughput. Amazon also supports ["Provisioned Concurrency"](https://docs.aws.amazon.com/lambda/latest/dg/configuration-concurrency.html) which keeps a certain number of Lambdas ready for execution, which adds another dimension to price. 

I have found this to be significantly simpler than cost projections using long lived resources. Accurately performing cost projections on long lived resources requires benchmarking in a prod-like environment to understand throughput. It requires correct instances sizing and monitoring of system level resources, which is time consuming and a largely manual process. Any changes to instances sizing, or shifting workloads necessitates repeating this process! The simplicity and predictability of pricing makes it trivial for anyone to perform Lambda price projections at the beginning of projects, and for the company to understand how costs will scale with traffic.

# Deployment velocity

Lambda deployment only requires:

**Package a Lambda function as a zip file and put it in a known S3 location**

That’s it. The next Lambda invoked will use the most recent s3 zip file. Any current Lambdas will finish their invocations and then use the new code. This enables rapid feedback. It also makes rollbacks trivial; just put a previous version of the zip file in s3. In my experience deploying a lambda takes < 1 minute!

# Forced Structure - Development Velocity

Lambda imposes a number of constraints in order to execute a lambda on AWS. Lambdas must:

- Be configured through environmental variables
- Accept known structured payloads and require a specific call signature

This enables quick development velocity. The Lambdas I work on use Golang and Amazon provides strict types for all Lambda inputs. Tests use well defined contracts and receive the exact same input and types that Amazon provides at runtime. Verifying a function locally using a unit test provides a very high level of confidence the function will work on Lambda. The failure domain for deploys is minimized to:

- Environmental configuration
- IAM permissions

I have found that these failures are solved a single time and then are pretty much stable.

# Conclusion

Lambda has been revolutionary and has enabled rapid iteration and deployment, while removing a whole class of failure domains. I’ve found lambda to be: reliable, predicable, simple, structured, and cost effective. Lambda is the closest solution to my idea developer experience. Even with the potential for function sprawl, I think it’s a net positive for the industry and can't wait to see what companies do with it! 
