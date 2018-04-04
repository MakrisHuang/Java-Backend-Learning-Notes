# Spring Boot
不得不說Spring Boot真的很強，一堆雜七雜八的配置都可以自動決定。不過還是有一些東西需要釐清

### 註解相關
* ``@EnableAuthConfiguartion`` vs ``@ComponentScan``

``@EnableAuthConfiguartion``是告訴Spring Boot說我要啟動自動配置（譬如說用spring-boot-starter-web的起步依賴）；而``@ComponentScan``就是掃描你使用的類，所以這兩個可以並存不衝突的

* ``@SpringBootApplication``

要在Main.class加入這註解才能啟動

*	如何在Test中啟用Spring Boot？同時使用以下註解
	* ``@RunWith(SpringRunner.class)``
	* ``@SpringBootTest(classes = ApplicationConfiguration.class) //自定義配置類``

	