
# 필요 디펜던시
1. nest/typeORM
2. typeORM
3. DB 클라이언트(sqlite, mysql 등등)
# 절차

## TypeORM Module 을 앱 모듈 에 넣는다.

- 이 작업은 어플리케이션마다 1회만 하면 된다.
- synchronize 옵션에 주의. 개발환경 only. [Auto Migration!!!!]
```

@Module({
  imports: [TypeOrmModule.forRoot({
    type:'sqlite',
    database:'db.sqlite',
    entities:[],
    synchronize:true
  }),

    UsersModule, ReportsModule],

  controllers: [AppController],

  providers: [AppService],

})

export class AppModule {}
```

## 엔티티 파일의 작성
- 여기서부터는 각 모듈마다 따로 해줘야 하는 절차다.
```
import { Entity, Column, PrimaryGeneratedColumn } from "typeorm";

@Entity()
export class User{
    @PrimaryGeneratedColumn()
    id: number;
    @Column()
    email: string;
    @Column()
    password: string;
}
```

## 작성된 엔티티 파일을 개별 모듈에 임포트
```
import { TypeOrmModule } from '@nestjs/typeorm';
import { User } from './user.entity';
  
@Module({

  imports: [TypeOrmModule.forFeature([User])], //cause Repository
  controllers: [UsersController],
  providers: [UsersService]
})

export class UsersModule {}
```

## 앱 모듈의 타입ORM에 엔티티 넣기
```
@Module({
  imports: [TypeOrmModule.forRoot({
    type:'sqlite',
    database:'db.sqlite',
    entities:[User], //이것
    synchronize:true
  }),
  UsersModule, ReportsModule],
  controllers: [AppController],
  providers: [AppService],
})

export class AppModule {}
```

