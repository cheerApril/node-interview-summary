# node-interview-summary
<br> JS常见的设计模式:
<br> -- 1.单例模式 保证一个类仅有一个实例，并提供一个访问它的全局访问点
<br> -- 2.策略模式 定义一系列的算法，把它们一个个封装起来，并且使它们可以相互替换。(eg: 设计状态码 {状态码:"错误信息"})
<br> -- 3.代理模式 为一个对象提供一个代用品或占位符，以便控制对它的访问 (eg: 买股票:代理的对象(股票投资顾问)帮客户购入股票的时候,查看这个股票是否能购入,判断可以购入,再确认客户是否真的购入,才完成购入的操作)
<br> -- 4.迭代器模式 迭代器模式是指提供一种方法顺序访问一个聚合对象中的各个元素，而又不需要暴露该对象的内部表示。(数组for..of, forEach, map这些遍历方法)
<br> -- 5.发布-订阅模式 也称作观察者模式，定义了对象间的一种一对多的依赖关系，当一个对象的状态发 生改变时，所有依赖于它的对象都将得到通知 (eg: Android的onclickListener 点击事件)
<br> -- 6.命令模式 用一种松耦合的方式来设计程序，使得请求发送者和请求接收者能够消除彼此之间的耦合关系.命令（command）指的是一个执行某些特定事情的指令
<br> -- 7.组合模式 是用小的子对象来构建更大的 对象，而这些小的子对象本身也许是由更小 的“孙对象”构成的。
<br> -- 8.模板方法模式 模板方法模式由两部分结构组成，第一部分是抽象父类，第二部分是具体的实现子类。(继承类似的概率)
<br> -- 9.享元模式 享元（flyweight）模式是一种用于性能优化的模式，它的目标是尽量减少共享对象的数量
<br> -- 10.职责链模式 使多个对象都有机会处理请求，从而避免请求的发送者和接收者之间的耦合关系，将这些对象连成一条链，并沿着这条链 传递该请求，直到有一个对象处理它为止
<br> -- 11.中介者模式 所有的相关 对象都通过中介者对象来通信，而不是互相引用，所以当一个对象发生改变时，只需要通知中介者对象即可 (爸爸跟妈妈吵架了,他们不想互相说话,就让我去传话了.)
<br> -- 12.装饰者模式 以动态地给某个对象添加一些额外的职责，而不会影响从这个类中派生的其他对象。是一种“即用即付”的方式，能够在不改变对 象自身的基础上，在程序运行期间给对象动态地 添加职责
<br> -- 13.状态模式 事物内部状态的改变往往会带来事物的行为改变。在处理的时候，将这个处理委托给当前的状态对象即可，该状态对象会负责渲染它自身的行为(eg: 人在清醒状态做什么(工作,吃饭), 人在疲惫的时候做什么(睡觉,休息))
<br> -- 14.适配器模式 是解决两个软件实体间的接口不兼容的问题，对不兼容的部分进行适配 (eg:判断数据类型,string的做什么处理,array做什么处理)
<br> -- 15.外观模式 为子系统中的一组接口提供一个一致的界面，定义一个高层接口，这个接口使子系统更加容易使用

<br> Mysql 相关方面:
<br> -----Mysql建表规则:
<br> -------1.创建表时必须显式指定字符集为utf8或utf8mb4。
<br> -------2.创建表时必须显式指定表存储引擎类型，如无特殊需求，一律为InnoDB。(下面会了解一下常见的搜索引擎)
<br> -------3.强制主键为Id,类型为int或bigInt,而且是自增 auto_increment
<br> -------4.尽量创建数据库字段的时候避免null,设置not null,如果需求需要这个字段可以为空,那也可以为他设置default.
<br> -------5.必须创建create_time跟update_time相关字段.
<br> -------6.表达是与否概念的字段，必须使用is_xxx的方式命名，数据类型是unsigned tinyint（1表示是，0表示否).(布尔类型的值均以 is、has、exist 或者 can开头.这个挺不错的)
<br> -------7.表名.字段名必须使用小写字母或数字，禁止出现数字开头，禁止两个下划线中间只出现数字。数据库字段名的修改代表很大，因为无法进行预发布，所以字段名称需要慎重考虑。(mysql 在window 下是不区分大小写但是Linux下是区分大小写的)
<br> -------8.【强制】主键索引名为pk字段名；唯一索引名为uk字段名；普通索引名则为idx_字段名(pk_即primary key；uk_即unique key；idx_即index的简称)
<br> -------9.【小数类型为decimal，禁止使用float和double。float和double的存储的时候，存在精度损失的问题，很可能在值的比较时，得到不正确的结果。如果存储的数据范围超过decimal的范围，建议将数据拆成整数和小数分开存储。
<br> -------10.【强制】如果存储的字符串的字符长度几乎相等，使用char定长字符串类型。
<br> -------11.【强制】varchar是可变长字符串，不预先分配存储空间，长度不要超过5000，如果存储长度大于此值，定义字段类型为text，独立出来一张表，用主键来对应，避免影响其它字段索引效率。(尽量不要吧字段定义成TEXT)
<br> -------12.【推荐】如果修改字段含义或对字段表示的状态追加时，需要及时更新字段注释。(这是一个很好的习惯)
<br> -------13. 为数据库字段增加comment是一个很好的习惯.
<br> -------13. 字段名字不要用驼峰命名法. 推荐使用create_time
 
<br> -------Mysql搜索引擎(mysql 8.0文档)
<br> ----Key Advantages of InnoDB
<br> Its  DML operations follow the ACID model, with transactions featuring commit, rollback, and crash-recovery capabilities to protect user data. (事务)
<br> Row-level locking and Oracle-style consistent reads increase multi-user concurrency and performance. (行锁)
<br> InnoDB tables arrange your data on disk to optimize queries based on primary keys. Each InnoDB table has a primary key index called the clustered index that organizes the data to minimize I/O for primary key lookups. (主键的复合索引减少I/O 并且加快查询)  
<br> To maintain data integrity, InnoDB supports FOREIGN KEY constraints. With foreign keys, inserts, updates, and deletes are checked to ensure they do not result in inconsistencies across different tables. (支持外键)

<br> -------git常用命令

<br> ------- 应用层

<br> ------- MQ消息队列
