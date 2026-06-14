# AWS 08 - Realtime Likes Microservice

This version builds on the independently deployable service architecture from version 07 and adds the realtime likes service.

## What changed in this version

- `services/realtime-likes-service` is added as its own deployable microservice.
- The service exposes realtime like analytics over API Gateway and WebSocket infrastructure.
- The UI analytics view combines historic buckets with realtime like updates.
- The realtime service owns its own CDK stack under `services/realtime-likes-service/cdk`.

## Deployable units

- `apps/ui`
- `services/cognito-service`
- `services/photos-service`
- `services/historic-likes-service`
- `services/realtime-likes-service`

Deploy the realtime service independently:

```bash
pnpm -C services/realtime-likes-service run deploy
```

Deploy the full version:

```bash
pnpm run deploy-everything
pnpm run generate-env
pnpm run website:deploy
```

## Local workflow

```bash
pnpm install
pnpm run type-check
pnpm run bootstrap-up
pnpm run data:seed
pnpm run simulator:start
```

The UI reads photos, historic likes, realtime likes, WebSocket, and Cognito settings from SSM via:

```bash
pnpm -C apps/ui run generate-env
```

## Structure

```text
apps/ui/cdk
services/cognito-service/cdk
services/photos-service/cdk
services/historic-likes-service/cdk
services/realtime-likes-service/cdk
packages/events
scripts
```

