<h1 align="center"></h1>

<div align="center">
  <a href="http://nestjs.com/" target="_blank">
    <img src="https://nestjs.com/img/logo_text.svg" width="150" alt="Nest Logo" />
  </a>
</div>

<h3 align="center">NestJS Loki Logger</h3>

<div align="center">
<a href="https://www.npmjs.com/package/@djeka07/nestjs-loki-logging"><img src="https://img.shields.io/npm/v/@djeka07/nestjs-loki-logging.svg" alt="NPM Version" /></a>
<a href="https://www.npmjs.com/package/@djeka07/nestjs-loki-logging"><img src="https://img.shields.io/npm/l/@djeka07/nestjs-loki-logging.svg" alt="Package License" /></a>


  <a href="https://nestjs.com" target="_blank">
    <img src="https://img.shields.io/badge/built%20with-NestJs-red.svg" alt="Built with NestJS">
  </a>
</div>

### Introduction
A logger that logs to Grafana Loki. 
### Installation

```bash
yarn add @djeka07/nestjs-loki-logger
```

### Usage

#### Importing module

```typescript
import { LokiLoggerModule } from '@djeka07/nestjs-loki-logger';
@Module({
  imports: [
    LokiLoggerModule.forRoot({
      app: 'app-name',
      host: 'host',
      userId: 'user id',
      password: 'password',
      environment: 'development' | 'production', // Optional, defaults to production
      logDev: false, // Optional, default to false
      minLogLevel: LogLevel.verbose, // Optional, defaults to LogLevel.verbose
    }),
  ],
  providers: [],
  exports: [],
})
export class AModule {}
```

#### Importing module Async

```typescript
import { LokiLoggerModule } from '@djeka07/nestjs-loki-logger';
@Module({
  imports: [
    LokiLoggerModule.forAsyncRoot({
      useFactory: async () => {
        return {
          app: 'app-name',
          host: 'host',
          userId: 'user id',
          password: 'password',
          environment: 'development' | 'production', // Optional, defaults to production
          logDev: false, // Optional, default to false
          minLogLevel: LogLevel.verbose, // Optional, defaults to LogLevel.verbose
        };
      },
    }),
  ],
  providers: [],
  exports: [],
})
export class AModule {}
```

#### Add logger to nest logging

```typescript
import { NestFactory } from '@nestjs/core';
import { MainModule } from './main.module';
import { LokiLoggerService } from '@djeka07/nestjs-loki-logger';


async function bootstrap() {
  const app = await NestFactory.create(MainModule, {
    bufferLogs: true,
  });
  app.useLogger(app.get(LokiLoggerService));
  await app.listen(3000, '0.0.0.0');
}
bootstrap();
```

#### Use the log service

```typescript
import { LokiLoggerService } from '@djeka07/nestjs-loki-logger';

@Injectable()
export class AService {
  constructor(private readonly loggerService: LokiLoggerService) {
    this.loggerService.verbose('message', [{ optionalProps: 'optionalProps' }])
  }
}
```

## Author
**André Ekbom [Github](https://github.com/djeka07)**

## License

Licensed under the MIT License - see the [LICENSE](LICENSE) file for details.