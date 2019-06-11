```
<?xml version="1.0" encoding="UTF-8" ?>
<!-- 如果配置文件 logback-test.xml 和 logback.xml 都不存在,那么 logback 默认地会调用BasicConfigurator,创建一个最小化配置.
     最小化配置由一个关联到根 logger 的ConsoleAppender 组成.输出用模式为
              %d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n
     的 PatternLayoutEncoder 进行格式化。root logger 默认级别是 DEBUG。 -->
<!-- logback整合日志-->
<!-- 根节点：configuration包含以下三个属性
             1.scan: 当此属性设置为true时，配置文件如果发生改变，将会被重新加载，默认值为true。
             2.scanPeriod: 设置监测配置文件是否有修改的时间间隔，如果没有给出时间单位，默认单位是毫秒。
                           当scan为true时，此属性生效。默认的时间间隔为1分钟。
             3.debug: 当此属性设置为true时，将打印出logback内部日志信息，实时查看
                      logback运行状态。默认值为false。-->
<configuration scan="true" scanPeriod="60 seconds" debug="false">
    <!-- 子节点 -->
    <!-- 1.子节点<contextName>：用来设置上下文名称，每个logger都关联到logger上下文，默认上下文名称为default。
           但可以使用<contextName>设置成其他名字，用于区分不同应用程序的记录。一旦设置，不能修改。-->
    <!--<contextName>myAppName</contextName>-->

    <!-- <include> 标签在一个配置文件中包含另外一个配置文件 -->
    <!--<include resource="org/springframework/boot/logging/logback/base.xml"/>-->

    <!-- 2.子节点<property> ：用来定义变量值，它有两个属性name和value，通过<property>定义的值会被插入到logger上下文中，
           可以使“${}”来使用变量。-->
    <!-- 定义日志文件 输入位置 -->
    <property name="log_dir" value="${LOG_PATH}"/>
    <!--<property name="log_dir" value="/opt/Log/prom_prize" />-->
    <!-- 日志最大的历史 30天 -->
    <property name="maxHistory" value="30"/>

    <!-- 3.子节点<timestamp>：获取时间戳字符串，他有两个属性key和datePattern
           key: 标识此<timestamp> 的名字；
　　　　    datePattern: 设置将当前时间（解析配置文件的时间）转换为字符串的模式，遵循java.txt.SimpleDateFormat的格式。-->
    <!--<timestamp key="bySecond" datePattern="yyyyMMdd'T'HHmmss"/>-->

    <!-- 4.子节点<appender>：负责写日志的组件，它有两个必要属性name和class。
              name指定appender名称，
              class指定appender的全限定名-->
    <!-- Appender主要用于指定日志输出的目的地，目的地可以是控制台、文件、远程套接字服务器、 MySQL、PostreSQL、 Oracle和其他数据库、 JMS和远程UNIX Syslog守护进程等。  -->
    <!--    4.1 ConsoleAppender  把日志输出到控制台，有以下子节点：
                          <encoder>：对日志进行格式化。
　　　　　　                <target>：字符串System.out(默认)或者System.err-->
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <!-- 对日志进行格式化 -->
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger -%msg%n</pattern>
        </encoder>
    </appender>

    <!--    4.2 FileAppender：把日志添加到文件，有以下子节点：
　　　　　　<file>：被写入的文件名，可以是相对目录，也可以是绝对目录，如果上级目录不存在会自动创建，没有默认值。
　　　　　　<append>：如果是 true，日志被追加到文件结尾，如果是 false，清空现存文件，默认是true。
　　　　　　<encoder>：对记录事件进行格式化。
　　　　　　<prudent>：如果是 true，日志会被安全的写入文件，即使其他的FileAppender也在向此文件做写入操作，效率低，默认是 false。-->
    <!--<appender name="FILE" class="ch.qos.logback.core.FileAppender">-->
<!--　　　　　<file>testFile.log</file>-->
<!--　　　　　<append>true</append>-->
<!--　　　　　<encoder>-->
<!--　　　　　　　<pattern>%-4relative [%thread] %-5level %logger{35} - %msg%n</pattern>-->
<!--　　　　　</encoder>-->
    <!--</appender>-->

    <!--    4.3 RollingFileAppender：滚动记录文件，先将日志记录到指定文件，当符合某个条件时，将日志记录到其他文件。有以下子节点：
                1)<file>：被写入的文件名，可以是相对目录，也可以是绝对目录，如果上级目录不存在会自动创建，没有默认值。
　　　　　　      2)<append>：如果是 true，日志被追加到文件结尾，如果是 false，清空现存文件，默认是true。
　　　　　　      3)<rollingPolicy>:当发生滚动时，决定RollingFileAppender的行为，涉及文件移动和重命名。属性class定义具体的滚动策略类
                    class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy"： 最常用的滚动策略，它根据时间来制定滚动策略，既负责滚动也负责出发滚动。有以下子节点：
　　　　　　　　           <fileNamePattern>：必要节点，包含文件名及“%d”转换符，“%d”可以包含一个java.text.SimpleDateFormat指定的时间格式，如：%d{yyyy-MM}。
                                           如果直接使用 %d，默认格式是 yyyy-MM-dd。RollingFileAppender的file字节点可有可无，通过设置file，可以为活动文件和归档文件
                                           指定不同位置，当前日志总是记录到file指定的文件（活动文件），活动文件的名字不会改变；如果没设置file，活动文件的名字会根据fileNamePattern
                                           的值，每隔一段时间改变一次。“/”或者“\”会被当做目录分隔符。
　　　　　　　　           <maxHistory>:可选节点，控制保留的归档文件的最大数量，超出数量就删除旧文件。假设设置每个月滚动，且<maxHistory>是6，则只保存最近6个月的文件，
                                           删除之前的旧文件。注意，删除旧文件是，那些为了归档而创建的目录也会被删除。
　　　　　　          class="ch.qos.logback.core.rolling.SizeBasedTriggeringPolicy"： 查看当前活动文件的大小，如果超过指定大小会告知RollingFileAppender
                                           触发当前活动文件滚动。只有一个节点:
　　　　　　　　                             <maxFileSize>:这是活动文件的大小，默认值是10MB。
　　　　　　　　  4)<prudent>：当为true时，不支持FixedWindowRollingPolicy。支持TimeBasedRollingPolicy，但是有两个限制，1不支持也不允许文件压缩，2不能设置file属性，必须留空。
　　　　　　     5)<triggeringPolicy >: 告知 RollingFileAppender 合适激活滚动。
　　　　　　           class="ch.qos.logback.core.rolling.FixedWindowRollingPolicy" 根据固定窗口算法重命名文件的滚动策略。有以下子节点：
　　　　　　　　        <minIndex>:窗口索引最小值
　　　　　　　　        <maxIndex>:窗口索引最大值，当用户指定的窗口过大时，会自动将窗口设置为12。
　　　　　　　　        <fileNamePattern>:必须包含“%i”例如，假设最小值和最大值分别为1和2，命名模式为 mylog%i.log,会产生归档文件mylog1.log和mylog2.log。
                                  还可以指定文件压缩选项，例如，mylog%i.log.gz 或者 没有log%i.log.zip-->
    <!-- ERROR级别日志 -->
    <!-- 滚动记录文件，先将日志记录到指定文件，当符合某个条件时，将日志记录到其他文件 RollingFileAppender-->
    <appender name="ERROR" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 过滤器，只记录WARN级别的日志 -->
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>ERROR</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
        <!-- 最常用的滚动策略，它根据时间来制定滚动策略.既负责滚动也负责出发滚动 -->
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!--日志输出位置  可相对、和绝对路径 -->
            <fileNamePattern>${log_dir}/%d{yyyy-MM-dd}/dabashow-error.log</fileNamePattern>
            <!-- 可选节点，控制保留的归档文件的最大数量，超出数量就删除旧文件假设设置每个月滚动，且<maxHistory>是6，
            则只保存最近6个月的文件，删除之前的旧文件。注意，删除旧文件是，那些为了归档而创建的目录也会被删除-->
            <maxHistory>${maxHistory}</maxHistory>
        </rollingPolicy>

        <!-- 按照固定窗口模式生成日志文件，当文件大于20MB时，生成新的日志文件。窗口大小是1到3，当保存了3个归档文件后，将覆盖最早的日志。
        <rollingPolicy class="ch.qos.logback.core.rolling.FixedWindowRollingPolicy">
          <fileNamePattern>${log_dir}/%d{yyyy-MM-dd}/.log.zip</fileNamePattern>
          <minIndex>1</minIndex>
          <maxIndex>3</maxIndex>
        </rollingPolicy>   -->
        <!-- 查看当前活动文件的大小，如果超过指定大小会告知RollingFileAppender 触发当前活动文件滚动
        <triggeringPolicy class="ch.qos.logback.core.rolling.SizeBasedTriggeringPolicy">
            <maxFileSize>5MB</maxFileSize>
        </triggeringPolicy>   -->

        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger - %msg%n</pattern>
        </encoder>
    </appender>


    <!-- WARN级别日志 appender -->
    <appender name="WARN" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 过滤器，只记录WARN级别的日志 -->
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>WARN</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!-- 按天回滚 daily -->
            <fileNamePattern>${log_dir}/%d{yyyy-MM-dd}/dabashow-warn.log
            </fileNamePattern>
            <!-- 日志最大的历史 60天 -->
            <maxHistory>${maxHistory}</maxHistory>
        </rollingPolicy>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger - %msg%n</pattern>
        </encoder>
    </appender>


    <!-- INFO级别日志 appender -->
    <appender name="INFO" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 过滤器，只记录INFO级别的日志 -->
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>INFO</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!-- 按天回滚 daily -->
            <fileNamePattern>${log_dir}/%d{yyyy-MM-dd}/dabashow-info.log
            </fileNamePattern>
            <!-- 日志最大的历史 60天 -->
            <maxHistory>${maxHistory}</maxHistory>
        </rollingPolicy>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger - %msg%n</pattern>
        </encoder>
    </appender>


    <!-- DEBUG级别日志 appender -->
    <appender name="DEBUG" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 过滤器，只记录DEBUG级别的日志 -->
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>DEBUG</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!-- 按天回滚 daily -->
            <fileNamePattern>${log_dir}/%d{yyyy-MM-dd}/dabashow-debug.log
            </fileNamePattern>
            <!-- 日志最大的历史 60天 -->
            <maxHistory>${maxHistory}</maxHistory>
        </rollingPolicy>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger - %msg%n</pattern>
        </encoder>
    </appender>


    <!-- TRACE级别日志 appender -->
    <appender name="TRACE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 过滤器，只记录ERROR级别的日志 -->
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>TRACE</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!-- 按天回滚 daily -->
            <fileNamePattern>${log_dir}/%d{yyyy-MM-dd}/dabashow-trace.log
            </fileNamePattern>
            <!-- 日志最大的历史 60天 -->
            <maxHistory>${maxHistory}</maxHistory>
        </rollingPolicy>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger - %msg%n</pattern>
        </encoder>
    </appender>
    <!--输出到mysql数据库的appender配置     -->
    <!--<appender name="db" class="ch.qos.logback.classic.db.DBAppender">-->
        <!--<connectionSource-->
                <!--class="ch.qos.logback.core.db.DriverManagerConnectionSource">-->
            <!--<driverClass>com.mysql.jdbc.Driver</driverClass>-->
            <!--<url>jdbc:mysql://120.0.0.1:3306/logback_member?characterEncoding=utf8</url>-->
            <!--<user>root</user>-->
            <!--<password>123456789</password>-->
        <!--</connectionSource>-->
    <!--</appender>-->

    <!-- 5.子节点<logger>：用来设置某一个包或具体的某一个类的日志打印级别、以及指定<appender>。<logger>仅有一个name属性，一个可选的level和一个可选的addtivity属性。
                         可以包含零个或多个<appender-ref>元素，标识这个appender将会添加到这个logger.
                         name: 用来指定受此logger约束的某一个包或者具体的某一个类。
　　　　                  level: 用来设置打印级别，大小写无关：TRACE, DEBUG, INFO, WARN, ERROR, ALL和OFF，还有一个特殊值INHERITED或者同义词NULL，
                                代表强制执行上级的级别。 如果未设置此属性，那么当前logger将会继承上级的级别。
                         addtivity: 是否向上级logger传递打印信息。默认是true。同<logger>一样，可以包含零个或多个<appender-ref>元素，标识这个appender将会添加到这个loger。-->
    <!-- Logger作为日志的记录器，把它关联到应用的对应的context上后，主要用于存放日志对象，也可以定义日志类型、级别。 -->
    <logger name="com.apache.ibatis" level="TRACE"/>
    <logger name="java.sql.Connection" level="DEBUG"/>
    <logger name="java.sql.Statement" level="DEBUG"/>
    <logger name="java.sql.PreparedStatement" level="DEBUG"/>
    <logger name="ch.qos.logback"/>

    <!-- 就是这个监控了mybatis日志输出，配合上面的“dao” -->
    <logger name="dao" level="DEBUG"/>

    <!-- 6.子节点<root>:它也是<logger>元素，但是它是根logger,是所有<logger>的上级。只有一个level属性，因为name已经被命名为"root",
                       且已经是最上级了。
                       level: 用来设置打印级别，大小写无关：TRACE, DEBUG, INFO, WARN, ERROR, ALL和OFF，不能设置为INHERITED或者同义词NULL。 默认是DEBUG。-->
    <root level="INFO">
        <!-- 控制台输出 -->
        <appender-ref ref="STDOUT" />
        <!--<!– 文件输出 –>-->
        <appender-ref ref="ERROR" />
        <appender-ref ref="INFO" />
        <appender-ref ref="WARN" />
        <appender-ref ref="DEBUG" />
        <appender-ref ref="TRACE" />
    </root>

</configuration>
```