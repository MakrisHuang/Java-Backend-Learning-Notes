# Exception
錯誤處理一直是我覺得最麻煩的地方，但java的錯誤提示其實蠻多的，這邊釐清一些常見錯誤以及排除方法

#### Proxy代理機制
Spring IoC機制會有很多代理的class，有時候不知道錯誤來源可以從這方面去想，就會知道有些class並沒有被代理到

#### JNDI Source Not Found (datasource:xxx)
這很明顯是資料庫來源沒有找到。首先檢查資料庫host, username, password有沒有設定好，可以先用第三方軟體測試。再來可以檢查 Tomcat 中有沒有設定好 resource ，以及``DataSource Bean``有沒有正確載入等等。

之前最機車的就是 Tomcat 8 還要在 web.xml 設定 resource-ref ，搞超久...

####ClassNotDefException vs NoClassDefFoundError
前者是找不到該class檔案，後者是找不到class的定義

#### SQLException
通常是語法有錯

#### Lazy Load
在SQL中我們常需要讀出圖片或是和其他Table Join，可是往往會造成很大的負擔，因此現在有Lazy Load的方式。但這會造成Session提早關閉，解決方法如下

1. FetchType設為EAGER
2. 在``LocalContainerEntityManagerFactoryBean``載入
``adapter.setDatabasePlatform("org.hibernate.dialect.MySQL5InnoDBDialect");``