---
title: Gradle 기본 명령어 모음
date: 2020-05-25 10:26:20
tags: Gradle
---
## 자주 쓰는 Gradle 명령어 

### 단위 테스트 돌리기  

```bash
gradle test
```

### 단위 테스트는 건너뛰고 빌드하기

```bash
grade build -x test
```

#### 특정 하위프로젝트에 포함된 단위 테스트만 돌리기

```bash
gradle :subproject:test
```

#### 특정 테스트 케이스만 돌리기

```bash
gradle test --tests *VerificationRepositoryTest*
```

#### 특정 하위프로젝트에 속한 특정 테스트 케이스만 돌리기

```bash
gradle :subproject:test --tests *VerificationRepositoryTest*
```

### 특정 프로필을 활성화하기

이 기능은 다음과 같은 전제하에 작동한다. 

* **Spring Boot**를 사용한다. 
* 환경변수가 `gradle`을 통해 테스트 케이스까지 전달되도록 `build.gradle` 파일에 다음과 같은 코드를 추가한다. 
    ```gradle
    tasks.withType(Test) {         systemProperties = System.getProperties()     }
    ```

`dev`란 프로필을 활성화하고 빌드를 하려면

```bash
gradle -Dspring.profiles.active=dev build
```

### 애플리케이션 띄우기

```bash
gradle bootRun
```

또는 

```bash
./gradlew build && java -jar ./gate/build/libs/gate-spring-0.0.1-SNAPSHOT.jar
```

#### `dev` 프로필로 서버를 띄우기

```bash
gradle -Dspring.profiles.active=dev bootRun
```


### 의존성 확인하기

#### 루트 프로젝트의 의존성 확인하기 

```bash
gradle -q dependencies
```

####  특정 하위프로젝트의 의존성 확인하기

```bash
gradle -q dependencies subproject:dependencies
```
 