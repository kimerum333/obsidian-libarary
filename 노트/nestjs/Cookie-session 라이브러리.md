# 개요
- 쿠키 값을 읽어들여서 처리하는 도중 서버에서 그걸 변경 시, 해당 내역을 반영한 새 set-cookie를 만들어 응답에 포함시키는 라이브러리.

# 설치
```
npm install cookie-session
npm install @types/cookie-session
```

# 임포트
```
const cookieSession = require('cookie-session');
// common js 방식만 사용.

async function bootstrap(){
	app.use(cookieSession({
		keys:["asdsdfs"]
	}))
}
```

# 사용
```
  @Post('/signup')
  async createUser(@Body() body: CreateUserDto ,@Session()session: any) {
    const user = await this.authService.signup(body.email,body.password);
    session.userId = user.id;
    return user;
  }
```
