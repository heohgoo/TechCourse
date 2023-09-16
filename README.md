# TechCourse

2021년 2월 우아한테크세미나

## <p style="text-align: center">SpringBoot</p>

#### 빌드

> - `프로젝트 생성` => **http://start.spring.io (Spring initializer)**
> 
>   SpringBoot version : SNAPSHOT(개발 중인 버전), M(MileStone), RC(Release Candidate), **GA(General Available)**
> - `의존성 관리`
>
>   특정한 버전을 명시하지 않더라도 라이브러리를 어떻게 가져오는가, 의존성을 관리하는가
>   
>   => gradle 파일이나 pom 파일에 해당 스프링부트에 대한 가장 잘 맞는(호환성이 좋은) 라이브러리를 정의해 두었다.
>   
>   스프링부트에서 관리해주는 라이브러리는 오히려 버전을 명시하지 않는 것이 나을 수 있다.(ex) lombok, spring-boot-start-...)
> - `애플리케이션 패키징 및 실행`
>
>   - mvn spring-boot:run, gradle bootRun => `Maven이나 Gradle 플러그인`을 사용해서 실행
>   - main 클래스 실행 => `IDE 환경`에서 실행, 가장 일반적이다.
>   - JAR 패키징 & java -jar => 스프링부트 플러그인으로 특수한 형태의 JAR 파일로 패키징하고 실행, `서버에 배포`하는 용도
>
>     패키징을 통해 생성되는 JAR 파일 => fat jar, uber jar : 하나의 JAR 파일에 패키지와 모든 의존성을 포함하여 정의한다.


#### 코딩

> - 개발 툴 제공
>
>  `Spring-Boot-Devtools`
>
>   - 코드를 바꾸고 다시 build하면 자동으로 애플리케이션을 재시작하며 브라우저에도 업데이트해준다.(watcher 매커니즘)
>
>   - `Property Defaults, Automatic Restart, Live Reload, Global Settings, Remote Applications`
>
>   - 캐싱과 같은 기능 때문에 해당 의존성을 포함하여 패키징하여 배포 시 효율과 성능이 떨어지지 않을까?
>     괜찮다. JAR 배포 시 개발용인 Devtools 설정을 무시하기 때문에 의존성을 포함해도 된다.   
> - 자동 설정(Convention over Configuration)
> - 외부 설정


#### 배포 및 관리

> - 도커 이미지 생성
> - Actuator
> - 스프링부트 어드민
