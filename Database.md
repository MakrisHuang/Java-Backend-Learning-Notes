# Database
這邊介紹JPA, MyBatis以及Redis, EhCache等NoSQL的設定和注意事項

#### JPA
在多對多關係中，我們會生出一張新的表來讓兩邊join，而用JPA要注意``@ManyToMany``中的``joinColumn``以及``inverseColumn``必須對應好才能查到資料

``@JpaRepository``和``@CRUDRepository``的關係：前者extends自後者，後者單純只做CRUD

#### MyBatis
resultMap中可化簡resultType中的role_name as roleName的語法

#### Redis
使用lua腳本需注意``KEYS[]``和``ARGS[]``的傳入

#### EhCache
``@Cacheable``無法運作→在Config.class中的ComponentScan掃描``@Service``(放EhCache的地方)

需加入``spring-context-support 4.1.5.RELEASE``方可運作