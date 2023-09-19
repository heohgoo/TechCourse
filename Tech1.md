# TechCourse

2021년 2월 우아한테크세미나 => https://www.youtube.com/watch?v=z0EaPjF3pCQ

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

> - `개발 툴 제공`
>
>    `Spring-Boot-Devtools`
>
>   - 코드를 바꾸고 다시 build하면 자동으로 애플리케이션을 재시작하며 브라우저에도 업데이트해준다.(watcher 매커니즘)
>
>   - `Property Defaults, Automatic Restart, Live Reload, Global Settings, Remote Applications`
>
>   - 캐싱과 같은 기능 때문에 해당 의존성을 포함하여 패키징하여 배포 시 효율과 성능이 떨어지지 않을까?
>     괜찮다. JAR 배포 시 개발용인 Devtools 설정을 무시하기 때문에 의존성을 포함해도 된다.   
> - `자동 설정(Convention over Configuration)`
>
>   `애플리케이션에서 설정한 빈 등록`
>   - @ComponentScan
>   - @Component, @Service, @Controller, @Repoistory
>   - @Configuration => Bean 새롭게 정의
>   - @Bean
>
>   `자동 설정으로 제공하는 빈 등록`
>   - 패키지 간 ComponentScan
>   - META-INF/spring.factories
>   - EnableAutoConfiguration
>   - @Configuration && @ConditionalOnXxx
> - `외부 설정(코드에서 값을 외부로 꺼내온다.)`
>   - `application.properties`, `application.yaml` => JSON 형식에서 중괄호가 빠진 것(yaml), 환경 변수, java 명령어 아규먼트 키/값 형태로 정의되어 있는 다양한 외부 설정 지원 => @ConfigurationProperties
>   - 가장 구체적이고`(config 디렉토리 안에 있으면 더욱 구체적이다.)` 가까운 위치`(현재 파일 시스템에 가까울수록, JAR 파일보다는 멀수록)`에 있는 설정의 우선 순위가 높다. => properties들중 우선순위가 높은 것이 덮어쓰는 형식이다.
>   - application.properties 설정 중 한글이 필요한 경우 encoding 설정을 통해 utf-8을 아스키로 변환하면 깨짐 현상을 없앨 수 있다.(자바 스펙 이슈)


#### 배포 및 관리

> - `도커 이미지 생성(계층형 이미지 빌드 지원)`
>   - 도커 정리 => https://github.com/heohgoo/DockerStudy
>   - 도커 이미지는 다른 이미지를 기반으로 새로운 이미지를 만들 수 있다.
>   - 계층형 이미지를 만든다면 `기존 계층은 캐시로 재사용`할 수 있어 효율적이다.
>     메모리가 큰 fat JAR를 매번 빌드하는 대신 기존 계층을 재사용할 수 있도록 한다. 바뀐 계층부터 새롭게 빌드하는 형식이다.
>   - 스프링부트 이미지 생성(`spring-boot-build-image`)
>     <br>
      <br>
>     ![image](https://github.com/heohgoo/TechCourse/assets/95553132/af5e6f41-1be6-4c7e-a2a3-eff53f1890db)
>   - 이미지의 계층 구조 확인 => dive {image name} (`docker dive opensource`) => https://github.com/wagoodman/dive
> - `Actuator(관리)` => 애플리케이션 `관련 데이터 및 모니터링 정보` 제공
>   - 웹(JSON)과 JMX 지원(`spirng-boot-starter-actuator`) => "url../actuator" => self-descripted(restful api의 특성)
>   - management.endpoints.web.exposure.include = *(모든 endpoint를 확인할 수 있다.) => application.properties에 구문 추가
>   - 여러 엔드포인트 제공
>     - /beans, /configprops(property 조회), /logger(로그), /heapdump(메모리의 현재 상태), /threaddump(스레드의 현재 상태), .. 
>     - `런타임 중에도 logger의 level을 바꿀 수 있다. (ex) configuredLevel -mode)`
> - `스프링부트 어드민(Actuator 기반 UI 오픈소스)` => https://github.com/codecentric/spring-boot-admin
>   - 애플리케이션 내부의 Actuator 정보를 admin 서버로 보내서 admin 서버에서 모니터링이 가능하게 한다.
