# Koa Health Check

Cloud Health Connect provides a Middleware based on
[Cloud Health](https://github.com/CloudNativeJS/cloud-health) for use with Koa a:

- Health Endpoint
- Liveness Endpoint
- Readiness Endpoint

to enable services and applications for use with Kubernetes.

## Usage

```typescript
import * as Koa from 'koa';
import * as health from '@cloudnative/health';
import { HealthEndpoint, ReadinessEndpoint, LivenessEndpoint } from 'koa-health-check';

const healthcheck = new health.HealthChecker();
const koa = new Koa();

koa.all('/live', LivenessEndpoint(healthcheck));
koa.all('/ready', ReadinessEndpoint(healthcheck));
koa.all('/health', HealthEndpoint(healthcheck));
```

## Status Responses

| Cloud Health Status | Readiness Status Code | Liveness Status Code | Combined Health Status Code |
|---------------------|-----------------------|----------------------|-----------------------------|
| STARTING            | 503 UNAVAILABLE       | 200 OK               | 503 UNAVAILABLE             |
| UP                  | 200 OK                | 200 OK               | 200 OK                      |
| DOWN                | 503 UNAVAILABLE       | 503 UNAVAILABLE      | 503 UNAVAILABLE             |
| STOPPING            | 503 UNAVAILABLE       | 503 UNAVAILABLE      | 503 UNAVAILABLE             |
| STOPPED             | 503 UNAVAILABLE       | 503 UNAVAILABLE      | 503 UNAVAILABLE             |
| -		              | 500 SERVER ERROR      | 500 SERVER ERROR     | 500 SERVER ERROR            |

## Development

To build the library, use `npm run build` command

To run the tests, use `npm run test` command
