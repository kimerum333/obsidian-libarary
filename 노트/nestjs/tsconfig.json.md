# 샘플 코드
```
{

    "compilerOptions": {
        "module": "CommonJS",
        "target": "ES2017",
        "experimentalDecorators": true,
        "emitDecoratorMetadata": true

    }

}
```


# experimentalDecorators 란?

        "experimentalDecorators": true,
        "emitDecoratorMetadata": true
 
 - nest 의 핵심 개념.
 - 본래 TS=> JS 컴파일 과정에서 소실되어야 할 타입 관련 정보를 데코레이터를 활용해 보존한다.