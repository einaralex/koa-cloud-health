# Koa Health Check

![npm](https://img.shields.io/npm/v/@restorecommerce/koa-health-check.svg?style=flat-square)[![Build Status][build]](https://travis-ci.org/restorecommerce/koa-cloud-health?branch=master)[![Dependencies][depend]](https://david-dm.org/restorecommerce/koa-cloud-health)[![Coverage Status][cover]](https://coveralls.io/github/restorecommerce/koa-cloud-health?branch=master)

[version]: http://img.shields.io/npm/v/koa-cloud-health.svg?style=flat-square
[build]: http://img.shields.io/travis/restorecommerce/koa-cloud-health/master.svg?style=flat-square
[depend]: https://img.shields.io/david/restorecommerce/koa-cloud-health.svg?style=flat-square
[cover]: http://img.shields.io/coveralls/restorecommerce/koa-cloud-health/master.svg?style=flat-square

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
| -		                | 500 SERVER ERROR      | 500 SERVER ERROR     | 500 SERVER ERROR            |

## Development

To build the library, use `npm run build` command

To run the tests, use `npm run test` command
