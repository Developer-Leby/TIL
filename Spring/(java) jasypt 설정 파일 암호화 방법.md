## Jasypt (Java Simplified Encryption)

- properties 또는 yaml 파일 정보의 보안을 위해 암호화를 제공해주는 라이브러리

  (데이터베이스 접속 정보, 외부로 노출되면 안되는 중요한 설정 정보)



1. **pom.xml에 dependency 설정**

   ~~~xml
   <dependency>
       <groupId>com.github.ulisesbocchio</groupId>
       <artifactId>jasypt-spring-boot-starter</artifactId>
       <version>2.1.0</version>
   </dependency>
   ~~~

2. **JasyptConfiguration.java 클래스 파일 생성**

   ~~~java
   public class JasyptConfiguration {
   	private static final String ENCRYPT_KEY = "selvas";
     
   	@Bean("jasyptStringEncryptor")
       public StringEncryptor stringEncryptor() {
           PooledPBEStringEncryptor encryptor = new PooledPBEStringEncryptor();
           SimpleStringPBEConfig config = new SimpleStringPBEConfig();
           config.setPassword(ENCRYPT_KEY); //암호화에 사용할 키 -> 중요
           config.setAlgorithm("PBEWithMD5AndDES"); //사용할 알고리즘
           config.setKeyObtentionIterations("1000");
           config.setPoolSize("1");
           config.setProviderName("leby");
           config.setSaltGeneratorClassName("org.jasypt.salt.RandomSaltGenerator");
           config.setStringOutputType("base64");
           encryptor.setConfig(config);
           return encryptor;
       }
   }
   ~~~

3. **application.yaml 또는 properties에 자바 빈 객체 설정**

   ~~~yaml
   jasypt:
     encryptor:
       bean: jasyptStringEncryptor
       password: selvas
   ~~~

4. **기존 데이터베이스 접속 정보**

   ~~~yaml
   spring:
     datasource:
       hikari:
         jdbc-url: jdbc:log4jdbc:mysql://localhost:3306/ocr_server?useSSL=false&serverTimezone=UTC&allowMultiQueries=true
         username: test
         password: leby1234!
   ~~~

5. **암호화 데이터 얻기**

   ~~~java
   @SpringBootApplication
   public class FinancialWebServerApplication implements CommandLineRunner {
   
   	@Autowired
   	DeleteFileScheduler deleteFileScheduler;
   	
   	private static final String ENCRYPT_KEY = "selvas";
   	
   	public static void main(String[] args) {
   		SpringApplication.run(FinancialWebServerApplication.class, args);
   	}
   	
   	@Override
   	public void run(String... args) throws Exception {
   		StandardPBEStringEncryptor pbeEnc = new StandardPBEStringEncryptor();
   		pbeEnc.setAlgorithm("PBEWithMD5AndDES");
   		pbeEnc.setPassword(ENCRYPT_KEY); //2번 설정의 암호화 키를 입력
   		
   		String url = "jdbc:log4jdbc:mysql://localhost:3306/ocr_server?useSSL=false&serverTimezone=UTC&allowMultiQueries=true"; 
   		String username = "test"; 
   		String password = "leby1234!"; 
   		System.out.println("암호화 URL :: " + pbeEnc.encrypt(url)); 
   		System.out.println("암호화 username :: " + pbeEnc.encrypt(username)); 
   		System.out.println("암호화 password :: " + pbeEnc.encrypt(password));
   
   	}
   }
   ~~~

6. **application.yaml 또는 properties에 암호화 사용 **

   - ENC(암호화 데이터)

   ~~~yaml
   spring:
     datasource:
       hikari:
         jdbc-url: ENC(7QjxeKNhnMbox81koBZw/PbMNvscfT5pjyBZJqQeRMNLSmmfC9sufavczbn3TuEYkwYrGxaFr6mxt+7SbaBhEdx/3U5EBbErDxMWe1VEhuKqisT+9xcs1skQZVintQIyvYhvzNHt2YPO/sh+nOsa3z2EzbgNWIl5X4yHZf8UykI=)
         username: ENC(ua/UBi3AaMsF9fZMptbc4w==)
         password: ENC(KVNU1LLtLdvQBHm4aYj8bo8s+Or48oeI)
   ~~~

   



