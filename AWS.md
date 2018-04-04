# Amazon Web Services (AWS) 
1. Spring Boot部署到AWS用``gradle``的``bootRepackage``命令，而非使用artifacts
2. 設定環境變數時需修改port為5000
3. 部署傳統Spring到Tomcat **8**時必須在專案檔的``web.xml``設定``resouece-ref``才能抓到mysql的資源
4. 