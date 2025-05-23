# 필요 디펜던시 설치
```
npm install class-validator class-transformer
```

# 절차
## main.ts 에서 사용 설정

```
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

import { ValidationPipe } from '@nestjs/common';

async function bootstrap() {

  const app = await NestFactory.create(AppModule);

  app.useGlobalPipes(
    new ValidationPipe({
      whitelist:true
    })

  )

  await app.listen(process.env.PORT ?? 3000);

}

bootstrap();
```

## DTO 작성
```
import { IsEmail,IsString,isString } from "class-validator";

  
  

export class CreateUserDto{

    @IsEmail()

    email:string;

    @IsString()

    password:string;

}
```

## 컨트롤러에서 검증요청
```
import { Body,Controller, Post } from '@nestjs/common';
import { CreateUserDto } from './dtos/create-user.dto';
  
@Controller('auth')
export class UsersController {
    @Post('/signup')
    createUser(@Body() body: CreateUserDto){
        console.log(body);
    }

}
```