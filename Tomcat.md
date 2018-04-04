# Tomcat
Tomcat一直以來都是Spring的啟動伺服器，可讓使用者上傳``jar``檔案來啟動App，非常方便

### 基本配置
1. 在``/lib``中加上``mysql-connector``才能讓Tomcat獲取MySQL資源
2. 於``/conf/context.xml``中添加resource，範例如下：

```
<Resource name="jdbc/XXXX"  <!-- 資料庫名稱 -->
type="javax.sql.DataSource"
	maxActive="20" maxIdle="5" maxWait="10000"
	username="user" password="password"
	driverClassName="com.mysql.jdbc.Driver"
	defaultTransactionIsolation="READ_COMMITTED"
	url="jdbc:mysql://hotname/XXXX" />
```

另外還記得把第三方套件丟到專案中的``/lib``資料夾，這樣Tomcat才能正確地使用他們，不然容易發生``NoClassDefFoundException``