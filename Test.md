# Test
如何做測試？可以依循一定的步驟去做：

1. 確定測試對象之行為、預期結果
2. 設定Test Cases，勁量涵蓋到邊界或極端情況
3. 寫測試

### Spring Boot下的測試
在測試類別中加入``@SpringBootTestApplication``來啟用，並可直接注入``@Service``等方便測試

### 好用的測試套件：JUnit
引入``assertEquals``可以比較多種型態，用法如下：

	import static org.junit.Assert.assertEquals; 