# RWDB
数据库读写分离<br/>
方案总共有3种<br/>
1.直接分离读写的mapper，配置不同的读写数据源<br/>
2.基于aop+反射注解（注解写在dao层）+Threadlocal实现数据源的更换<br/>
3.由于dao层的SQL语句或者方法可能重用较多，那方案2可能会变得不合适，可以基于业务层来实现数据源替换<br/>

另外mybatis做持久层的话有两种方案<br/>
1.通过Mybatis的Plugin在业务层实现数据库读写分离，在MyBatis创建Statement对象前通过拦截器选择真正的数据源，在拦截器中根据方法名称不同（select、update、insert、delete）选择数据源。<br/>
2.如果你的后台结构是spring+mybatis，可以通过spring的AbstractRoutingDataSource和mybatis Plugin拦截器实现非常友好的读写分离，原有代码不需要任何改变。推荐第四种方案<br/>
