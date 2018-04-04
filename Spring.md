# Spring

這份文件記錄配置Spring時常遇到的問題還有觀念解析

### Spring Initialization - 1
個人我覺得Spring在初始化比較複雜，簡單來說Spring收到請求後會轉發給 ``DispatchServlet`` ，所以要先初始化他。如何初始化？就是實現``ServletContextListener``的接口，該接口可由``ContextLoaderListener``實現。

另外要注意到的是，幾乎很多時候會用到``DispatchServlet``，故建議在系統啟動時就完成Spring IoC容器的初始化，這樣其他模組就能用享資源

早期Spring多用XML進行配置，後來在Servlet 3.0後因為取消web.xml配置，只能使用註解配置，因此在Spring 3.1後也提供Java註解配置。個人我也比較喜歡Java註解方式。

剛剛提到我們必須實現``ServletContextListener``及``DispatchServlet``，Spring為了提供更大的彈性，因此將這兩個初始化器包在``WebApplicationInitializer``類中，其中該類提供``onStartUp``方法來讓我們加載Configuration classes。

### Spring Initialization - 2
那這個onStartUp要放什麼？我們知道Spring是上下文關係的，因此可以使用``AnnotationConfigWebApplicationContext``類別來*註冊*每個Config.class。

從範例中我們可以看到我們先註冊``rootContext``，之後就可以針對不同的任務註冊Config.class，在管理上會方便許多

	AnnotationConfigWebApplicationContext rootContext = new AnnotationConfigWebApplicationContext();
    rootContext.register(RootContextConfiguration.class);
	container.addListener(new ContextLoaderListener(rootContext));
	container.addListener(SessionListener.class);
	
## Spring註解解釋
#### @Component vs. @Service vs. @Repository
從Spring Doc就可以看出@Component是屬於很廣泛的通稱

Annotation  | Meaning                                             
----------- | -----------------------------------------------------
@Component  | generic stereotype for any Spring-managed component 
@Repository | stereotype for persistence layer                    
@Service    | stereotype for service layer                        
@Controller | stereotype for presentation layer (spring-mvc)      

#### @ComponentScan
除了要掃描基本類別之外，也記得掃描要配置的特殊類別，不然就不會加載到IoC容器內，之前有一次要配置EhCache，卻忘記掃描他，所以就無法啟動（一個小時就不見了...)

## Spring Bean
1. 範圍：Singleton / Prototype / Global
2. 如何使用？在 @Service等高層次上使用 ``@Inject``注入Bean
3. Spring Bean可自定義生命週期中每個函數的功能（ex. 初始化或是銷毀該做什麼）

## Spring Configuration
這區塊記錄一些常見的小錯誤

* ``@ComponentScan``要放在Config.class
* 可以用``AnnotationConfigWebApplicationContext``來註冊Config.class
* **避免Conflict的方式：先檢查 Exception錯誤來源，之後換掉套件版本**
* ``Servlet``生命週期可作為判斷錯誤的來源
* 要載入外部變數時太慢：可讓Config.class實現``EnvironmentAware``接口，之後可用``Env.getProperty("name")``取得環境變數