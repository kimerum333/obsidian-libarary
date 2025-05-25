# canActivate()
- 가드 객체가 반드시 구현해야 하는 함수
- True 면 갈길 간다. False 면 막힌다.(403)

```
import { CanActivate, ExecutionContext } from '@nestjs/common';
import { Observable } from 'rxjs';

export class AuthGuard implements CanActivate{
    canActivate(context: ExecutionContext): boolean | Promise<boolean> | Observable<boolean> {
        const request = context.switchToHttp().getRequest();
        return request.session.userId;
    }
}
```

```
import {  UseGuards } from '@nestjs/common';
import { AuthGuard } from 'src/guards/auth.guard';

```