- 전반부를 진행했다면 레포지토리와 DB가 세팅된 상태일 것.
- 이제 실제로 그 DB를 DI받아 사용하는 법을 진행한다.

# 절차
## 서비스에 리포지토리를 DI
```
import { Injectable } from '@nestjs/common';
import { Repository } from 'typeorm';
import { InjectRepository } from '@nestjs/typeorm';
import { User } from './user.entity';

  

@Injectable()
export class UsersService {
    constructor(@InjectRepository(User) private repo: Repository<User>){
        this.repo = repo;
    }

    create(email:string, password:string){
        const user = this.repo.create({email,password});
        return this.repo.save(user);
    }
}
```
