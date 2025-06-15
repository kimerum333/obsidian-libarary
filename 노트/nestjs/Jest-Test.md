
# 테스트는 .spec.ts 에서.
- 기본 패턴
```
import { Test } from '@nestjs/testing';
import { AuthService } from './auth.service';
import { UsersService } from './users.service';

let service: AuthService;


//매번 서비스를 새로 만든다.
beforeEach(async()=>{
  const fakeUsersService = {
    find: () => Promise.resolve([]),
    create: (email: string, password: string) =>
      Promise.resolve({ id: 1, password }),
  };
  
  const module = await Test.createTestingModule({
    providers: [AuthService, {
        provide: UsersService,
        useValue:fakeUsersService
    }],
  }).compile();
  service = module.get(AuthService);
})

//각각의 it 구문이 @Test 에 해당
it('can create!', async () => {
  //create a fake copy of users service
  expect(service).toBeDefined();
});
```
