


### ����������

> �������ݱ��������ɶ�Ӧ��Model��Mapper��Service��Controller�򻯿���,��Ҫ����freemarker��Ϊģ������Service��Controller��

##### 1. ����������pom.xml����������jar��
```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>top.qilixiang</groupId>
  <artifactId>CodeGeneratorThree</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>jar</packaging>

  <name>CodeGeneratorThree</name>
  <url>http://maven.apache.org</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <freemarker.version>2.3.23</freemarker.version>
    <mybatis-generator.version>1.3.5</mybatis-generator.version>
    <mysql-connector-java.version>5.1.6</mysql-connector-java.version>
    <commons-lang3.version>3.5</commons-lang3.version>
    <slf4j-api.version>1.7.25</slf4j-api.version>
    <spring.baseline.version>4.3.10.RELEASE</spring.baseline.version>
    <logback.version>1.2.3</logback.version>
    <mybatis.mapper.version>3.3.9</mybatis.mapper.version>
    <mybatis.pagehelper.version>5.0.4</mybatis.pagehelper.version>
    <mybatis.version>3.4.2</mybatis.version>
    <junit.version>4.12</junit.version>
  </properties>

  <dependencies>

    <!--����������-->
    <dependency>
      <groupId>org.freemarker</groupId>
      <artifactId>freemarker</artifactId>
      <version>${freemarker.version}</version>
    </dependency>
    <dependency>
      <groupId>org.mybatis.generator</groupId>
      <artifactId>mybatis-generator-core</artifactId>
      <version>${mybatis-generator.version}</version>
    </dependency>

    <!--MyBatis-->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>${mybatis.version}</version>
    </dependency>
    <dependency>
      <groupId>tk.mybatis</groupId>
      <artifactId>mapper</artifactId>
      <version>${mybatis.mapper.version}</version>
    </dependency>
    <dependency>
      <groupId>com.github.pagehelper</groupId>
      <artifactId>pagehelper</artifactId>
      <version>${mybatis.pagehelper.version}</version>
    </dependency>

    <!--db-->
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>${mysql-connector-java.version}</version>
    </dependency>

    <!-- logger dependencies-->
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
      <version>${slf4j-api.version}</version>
    </dependency>
    <dependency>
      <groupId>ch.qos.logback</groupId>
      <artifactId>logback-core</artifactId>
      <version>${logback.version}</version>
    </dependency>
    <dependency>
      <groupId>ch.qos.logback</groupId>
      <artifactId>logback-classic</artifactId>
      <version>${logback.version}</version>
    </dependency>

    <!--commons-->
    <dependency>
      <groupId>org.apache.commons</groupId>
      <artifactId>commons-lang3</artifactId>
      <version>${commons-lang3.version}</version>
    </dependency>

    <!-- springFramework dependencies -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>${spring.baseline.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>${spring.baseline.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>${spring.baseline.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>${spring.baseline.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>${spring.baseline.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context-support</artifactId>
      <version>${spring.baseline.version}</version>
    </dependency>

    <!--junit-->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>${junit.version}</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
</project>

```
##### 2. ��Ҫ���������ļ�application-dev.properties��generatorConfig.xml
> application-dev.properties
```
#-------��Ŀ���ڵĸ�Ŀ¼---------
project.path=D:/code/project/CodeGeneratorThree

java.path=/src/main/java
resources.path=/src/main/resources
db.obj.Delimiter=`

gen.basepackage=top.qilixiang.crud
gen.context.id=crud
gen.author=qilixiang
rest=true

#-------Mapper�ӿ����ڵİ�---------
mappers=top.qilixiang.crud.base.Mapper

#-------���ݿ������---------
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/school?useUnicode=true&characterEncoding=utf8
jdbc.username=root
jdbc.password=123456


```
> generatorConfig.xml
```
<?xml version="1.0" encoding="UTF-8"?> <!DOCTYPE generatorConfiguration PUBLIC
    "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
    "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd"> <!-- ���������� -->
<generatorConfiguration>
  <properties resource="application-dev.properties"/>

  <context id="crud" defaultModelType="hierarchical" targetRuntime="MyBatis3Simple">

    <property name="autoDelimitKeywords" value="false"/>
    <property name="javaFileEncoding" value="UTF-8"/>
    <property name="javaFormatter" value="org.mybatis.generator.api.dom.DefaultJavaFormatter"/>
    <property name="xmlFormatter" value="org.mybatis.generator.api.dom.DefaultXmlFormatter"/>
    <property name="beginningDelimiter" value="${db.obj.Delimiter}"/>
    <property name="endingDelimiter" value="${db.obj.Delimiter}"/>
    <!-- mergeable Ϊtrueʱ���ɺϲ���Ϊfalse���������ɵ�ʱ���ø���-->
    <property name="mergeable" value="false"></property>
    <!--ͨ��mapper�Ĳ��-->
    <plugin type="tk.mybatis.mapper.generator.MapperPlugin">
      <property name="mappers" value="${mappers}"/>
    </plugin>

    <jdbcConnection driverClass="${jdbc.driver}" connectionURL="${jdbc.url}"
                    userId="${jdbc.username}" password="${jdbc.password}"/>
    <javaTypeResolver type="org.mybatis.generator.internal.types.JavaTypeResolverDefaultImpl">
      <property name="forceBigDecimals" value="false"/>
    </javaTypeResolver>
    <!--model-->
    <javaModelGenerator targetPackage="${gen.basepackage}.entity" targetProject="${project.path}${java.path}">
      <property name="constructorBased" value="false"/>
      <property name="enableSubPackages" value="true"/>
      <property name="immutable" value="false"/>
      <property name="trimStrings" value="true"/>
    </javaModelGenerator>
    <!--mapper xml file-->
    <sqlMapGenerator targetPackage="mapper" targetProject="${project.path}${resources.path}">
      <property name="enableSubPackages" value="false"/>
    </sqlMapGenerator>
    <!--Mapper interface-->
    <javaClientGenerator targetPackage="${gen.basepackage}.repository" type="XMLMAPPER"
                         targetProject="${project.path}${java.path}">
      <property name="enableSubPackages" value="false"/>
    </javaClientGenerator>

    <!--���CodeGenerator��ר��д������*�Ļ���ΪtableName��ǰ׺-->
    <table tableName="crud_*"  >
      <!--�������ɷ�ʽ-->
      <generatedKey column="id" sqlStatement="Mysql" identity="true"/>
    </table>

  </context>
</generatorConfiguration>

```

**ע�⣺**

- application-dev.properties��gen.context.id=crudҪ��generatorConfig.xml��<context id="crud */>"һ��
- CodeGeneratorҪ�����ݿ�ı���ǰ׺Ҫһ��

##### 3. ��Ҫ����freemarkerģ��������Service��Controller�ĸ�ʽ

> service.ftl
```
package ${basePackage}.service;

import com.github.pagehelper.ISelect;
import com.github.pagehelper.PageHelper;
import com.github.pagehelper.PageInfo;
import org.apache.ibatis.exceptions.TooManyResultsException;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.transaction.annotation.Transactional;
import tk.mybatis.mapper.entity.Condition;
import ${basePackage}.entity.${modelNameUpperCamel};
import ${basePackage}.repository.${modelNameUpperCamel}Mapper;

import java.lang.reflect.Field;
import java.lang.reflect.ParameterizedType;
import java.util.List;

/**
* ����ͨ��MyBatis Mapper�����Service�ӿڵ�ʵ��
*/
public class ${modelNameUpperCamel}Service{
    @Autowired
    protected ${modelNameUpperCamel}Mapper mapper;

    private Class<${modelNameUpperCamel}> modelClass;    // ��ǰ������ʵ���͵�Class

    public ${modelNameUpperCamel}Service() {
        ParameterizedType pt = (ParameterizedType) this.getClass().getGenericSuperclass();
        modelClass = (Class<${modelNameUpperCamel}>) pt.getActualTypeArguments()[0];
    }

    @Transactional(readOnly = false)
        public void save(${modelNameUpperCamel} model) {
        mapper.insertSelective(model);
    }

    @Transactional(readOnly = false)
    public void save(List<${modelNameUpperCamel}> models) {
        mapper.insertList(models);
    }

    @Transactional(readOnly = false)
        public void deleteById(Integer id) {
        mapper.deleteByPrimaryKey(id);
    }

    @Transactional(readOnly = false)
        public void deleteByIds(String ids) {
        mapper.deleteByIds(ids);
    }

    @Transactional(readOnly = false)
    public void update(${modelNameUpperCamel} model) {
        mapper.updateByPrimaryKeySelective(model);
    }

    public ${modelNameUpperCamel} findById(Integer id) {
        return mapper.selectByPrimaryKey(id);
    }


    public ${modelNameUpperCamel} findBy(String property, Object value) throws TooManyResultsException {
        // �ֶ���������Դ
        // DataSourceKeyHolder.setDbType(DataSourceKeyHolder.DataSourceType.MASTER);
        try {
            ${modelNameUpperCamel} model = modelClass.newInstance();
            Field field = modelClass.getDeclaredField(property);
            field.setAccessible(true);
            field.set(model, value);
            return mapper.selectOne(model);
        } catch (ReflectiveOperationException e) {
            throw new RuntimeException(e.getMessage(), e);
        }
    }

    public List<${modelNameUpperCamel}> findByIds(String ids) {
        return mapper.selectByIds(ids);
    }

    public List<${modelNameUpperCamel}> findByCondition(Condition condition) {
        return mapper.selectByCondition(condition);
    }


    public List<${modelNameUpperCamel}> findAll() {
        return mapper.selectAll();
    }

    public int count() {
        return mapper.selectCount(null);
    }


    public PageInfo findAll(Integer pageNumber, Integer pageSize) {
        return PageHelper.startPage(pageNumber, pageSize).doSelectPageInfo(new ISelect() {
            @Override
            public void doSelect() {
                mapper.selectAll();
            }
        });
    }
}

```
> controller-restful.ftl
```
package ${basePackage}.api;

import ${basePackage}.entity.${modelNameUpperCamel};
import ${basePackage}.service.${modelNameUpperCamel}Service;
import com.github.pagehelper.PageInfo;
import org.springframework.web.bind.annotation.*;

import javax.annotation.Resource;

/**
* Created by ${author} on ${date}.
*/
@RestController
@RequestMapping("${baseRequestMapping}")
public class ${modelNameUpperCamel}API {

    /**
     * �����ɹ�
     */
    private static final String DEFAULT_SUCCESS_MESSAGE = "SUCCESS";

    @Resource
    private ${modelNameUpperCamel}Service ${modelNameLowerCamel}Service;

    @PostMapping
    public String add(${modelNameUpperCamel} ${modelNameLowerCamel}) {
        ${modelNameLowerCamel}Service.save(${modelNameLowerCamel});
        return DEFAULT_SUCCESS_MESSAGE;
    }

    @DeleteMapping("/{id}")
    public String delete(@PathVariable Integer id) {
        ${modelNameLowerCamel}Service.deleteById(id);
        return DEFAULT_SUCCESS_MESSAGE;
    }

    @PutMapping
    public String update(${modelNameUpperCamel} ${modelNameLowerCamel}) {
        ${modelNameLowerCamel}Service.update(${modelNameLowerCamel});
        return DEFAULT_SUCCESS_MESSAGE;
    }
    @GetMapping("/{id}")
    public ${modelNameUpperCamel} detail(@PathVariable Integer id) {
        ${modelNameUpperCamel} ${modelNameLowerCamel} = ${modelNameLowerCamel}Service.findById(id);
        return ${modelNameLowerCamel};
    }

    @GetMapping
    public PageInfo list(Integer pageNumber, Integer pageSize) {
        PageInfo pageInfo = ${modelNameLowerCamel}Service.findAll(pageNumber,pageSize);
        return pageInfo;
    }
}

```


##### 4. ����CodeGenerator��
```
package top.qilixiang;

import freemarker.template.TemplateExceptionHandler;
import org.apache.commons.lang3.StringUtils;
import org.mybatis.generator.api.MyBatisGenerator;
import org.mybatis.generator.config.Configuration;
import org.mybatis.generator.config.Context;
import org.mybatis.generator.config.GeneratedKey;
import org.mybatis.generator.config.TableConfiguration;
import org.mybatis.generator.config.xml.ConfigurationParser;
import org.mybatis.generator.exception.InvalidConfigurationException;
import org.mybatis.generator.internal.DefaultShellCallback;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.core.io.ClassPathResource;
import org.springframework.core.io.Resource;

import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.sql.*;
import java.text.SimpleDateFormat;
import java.util.*;
import java.util.Date;

/**
 * �������������������ݱ��������ɶ�Ӧ��Model��Mapper��Service��Controller�򻯿�����<br/>
 * �ù�������ҪMBG�������ļ���properties�����ļ�<br />
 * ʹ�÷����ο�http://www.qilixiang1118.top
 *
 * @author qilixiang
 */
public class CodeGenerator {
    private static final Logger LOGGER = LoggerFactory.getLogger(CodeGenerator.class);

    //from constructor or keep default
    private String propertiesPath = "/application-dev.properties";
    private String configPath = "/generatorConfig.xml";

    //fields with default value
    private static final String BLANK_STRING = "";
    private final String DATE = new SimpleDateFormat("yyyy/MM/dd").format(new Date());//@date
    private final List<String> WARNINGS = new ArrayList<String>();
    private final DefaultShellCallback CALLBACK = new DefaultShellCallback(true);

    // from configuration
    private String AUTHOR;//@author
    private String CONTEXTID;
    private String PROJECT_PATH;
    //private final String TEMPLATE_FILE_PATH;
    private String BASE_PACKAGE;
    private String CONTROLLER_FTL;
    private String JAVA_PATH;
    private String RESOURCES_PATH;
    private String BASE_PACKAGE_PATH;
    private String PACKAGE_PATH_SERVICE;
    // private final String PACKAGE_PATH_SERVICE_IMPL;
    private String PACKAGE_PATH_CONTROLLER;
    private String JDBC_DIVER_CLASS_NAME;
    private String JDBC_URL;
    private String JDBC_USERNAME;
    private String JDBC_PASSWORD;

    //mbg config
    private Configuration config;
    private Context context;

    //freemarker config
    private freemarker.template.Configuration freemarkerCfg;
    private boolean need_rest;
    private boolean dealed = false;

    public CodeGenerator() {
        init();
    }

    public CodeGenerator(String propertiesPath, String mgbXmlPath) {
        this.propertiesPath = propertiesPath;
        this.configPath = mgbXmlPath;
        init();
    }

    private void init() {
        Resource resource = new ClassPathResource(propertiesPath);//ClassPathResource()�����ǵ�resourcesĿ¼�µ������ļ�
        Properties props = new Properties();
        try {
            props.load(resource.getInputStream());
            AUTHOR = props.getProperty("gen.author");
            CONTEXTID = props.getProperty("gen.context.id").trim();
            PROJECT_PATH = props.getProperty("project.path").trim();
            File projPathFile = new File(PROJECT_PATH);
            if (projPathFile.exists() == false) {
                projPathFile.mkdirs();
            }
            //TEMPLATE_FILE_PATH = PROJECT_PATH + "/src/test/resources/generator/template";
            BASE_PACKAGE = props.getProperty("gen.basepackage").trim();
            need_rest = Boolean.parseBoolean(props.getProperty("rest").trim());
            CONTROLLER_FTL = "controller" + (need_rest ? "-restful" : "") + ".ftl"; // controller.ftl
            JAVA_PATH = props.getProperty("java.path").trim();
            File javaPathFile = new File(PROJECT_PATH, JAVA_PATH);
            if (javaPathFile.exists() == false) {
                javaPathFile.mkdirs();
            }
            RESOURCES_PATH = props.getProperty("resources.path").trim();
            File resourcePathFile = new File(PROJECT_PATH, RESOURCES_PATH);
            if (resourcePathFile.exists() == false) {
                resourcePathFile.mkdirs();
            }
            BASE_PACKAGE_PATH = "/" + BASE_PACKAGE.replaceAll("\\.", "/") + "/";//��Ŀ������·��
            PACKAGE_PATH_SERVICE = BASE_PACKAGE_PATH + "service/";//���ɵ�Service���·��;
            // PACKAGE_PATH_SERVICE_IMPL = BASE_PACKAGE_PATH + "/service/impl/";//���ɵ�Serviceʵ�ִ��·�� ;
            if (need_rest)
                PACKAGE_PATH_CONTROLLER = BASE_PACKAGE_PATH + "/api/";//���ɵ�API���·��;
            else
                PACKAGE_PATH_CONTROLLER = BASE_PACKAGE_PATH + "/web/";//���ɵ�Controller���·��;

            JDBC_DIVER_CLASS_NAME = props.getProperty("jdbc.driver").trim();
            JDBC_URL = props.getProperty("jdbc.url").trim();
            JDBC_USERNAME = props.getProperty("jdbc.username").trim();
            JDBC_PASSWORD = props.getProperty("jdbc.password").trim();


            ConfigurationParser cp = new ConfigurationParser(WARNINGS);
            config = cp.parseConfiguration(new ClassPathResource(configPath).getInputStream());
            context = config.getContext(CONTEXTID);//CONTEXTID��generatorConfig.xml�е�<context id=""/>һ��

            //load jdbc driver
            Class.forName(JDBC_DIVER_CLASS_NAME);
        } catch (Exception e) {
            throw new RuntimeException();//ֱ���׳�����ʱ�쳣
        }
    }

    public void generateMapper() {
        dealTables();
        try {
            MyBatisGenerator myBatisGenerator = new MyBatisGenerator(config, CALLBACK, WARNINGS);
            myBatisGenerator.generate(null);
            if (LOGGER.isDebugEnabled()) {
                LOGGER.debug("����ɹ����ɣ�·����" + PROJECT_PATH);
            }
        } catch (InvalidConfigurationException | SQLException | IOException | InterruptedException e) {
            throw new RuntimeException();//ֱ���׳�����ʱ�쳣
        }
    }


    /**
     * ��������table���ã���ȷ�غ����ݿ��еı��Ӧ�������γ��µ�TableConfiguration�б�
     */
    private void dealTables() {
        if (!dealed) {
            List<TableConfiguration> tcs = context.getTableConfigurations();
            Set<TableConfiguration> newTcs = new HashSet<>();
            Set<String> dbTableNameSet = getDbTableNames();
            for (TableConfiguration tc : tcs) {
                dealTable(newTcs, dbTableNameSet, tc);
            }
            tcs.clear();
            tcs.addAll(newTcs);
            dealed = true;
        }
    }

    /**
     * ģ���ļ���·��
     *
     * @param templateDir
     */
    public void genServiceAndController(String templateDir) {
        dealTables();
        List<TableConfiguration> tableConfigs = context.getTableConfigurations();
        for (TableConfiguration conf : tableConfigs) {
            String domainName = conf.getDomainObjectName();
            try {
                //build config
                buildFreemarkerConfiguration(templateDir);
                //prepare data used in template
                Map<String, Object> data = new HashMap<>();
                data.put("date", DATE);
                data.put("author", AUTHOR);
                data.put("baseRequestMapping", tableNameConvertMappingPath(conf.getTableName()));
                data.put("modelNameUpperCamel", domainName);//??
                String modelNameLowerCamel = domainName.substring(0, 1).toLowerCase() + domainName.substring(1);
                data.put("modelNameLowerCamel", modelNameLowerCamel);
                data.put("basePackage", BASE_PACKAGE);

                String javaFileName = domainName + "Service.java";
                File file = new File(PROJECT_PATH + JAVA_PATH + PACKAGE_PATH_SERVICE + javaFileName);
                System.out.println(file);
                if (!file.getParentFile().exists()) {
                    file.getParentFile().mkdirs();
                }
                freemarkerCfg.getTemplate("service.ftl").process(data, new FileWriter(file));
                if (LOGGER.isDebugEnabled()) {
                    LOGGER.debug("·����" + PROJECT_PATH);
                    LOGGER.debug(javaFileName + "���ɳɹ�");
                }
                // File file1 = new File( PROJECT_PATH + JAVA_PATH + PACKAGE_PATH_SERVICE_IMPL + domainName + "ServiceImpl.java" );
                // if (!file1.getParentFile().exists()) {
                //   file1.getParentFile().mkdirs();
                // }
                // freemarkerCfg.getTemplate( "service-impl.ftl" ).process( data,
                //     new FileWriter( file1 ) );
                // System.out.println( domainName + "ServiceImpl.java ���ɳɹ�" );

                File file2 = new File(PROJECT_PATH + JAVA_PATH + PACKAGE_PATH_CONTROLLER + domainName + (need_rest ? "API" : "Controller") + ".java");
                if (!file2.getParentFile().exists()) {
                    file2.getParentFile().mkdirs();
                }
                //���ݿ����ǰ��ü�һ����ʶ��������CodeGenerator�Ĺ̶�д��
                freemarkerCfg.getTemplate(CONTROLLER_FTL).process(data, new FileWriter(file2));
                if (LOGGER.isDebugEnabled()) {
                    LOGGER.debug("·����" + PROJECT_PATH);
                    LOGGER.debug(domainName + (need_rest ? "API" : "Controller") + ".java ���ɳɹ�");
                }
            } catch (Exception e) {
                throw new RuntimeException();//ֱ���׳�����ʱ�쳣
            }
        }
    }


    private void buildFreemarkerConfiguration(String TEMPLATE_FILE_PATH) throws IOException {
        if (freemarkerCfg != null)
            return;
        freemarkerCfg = new freemarker.template.Configuration(freemarker.template.Configuration.VERSION_2_3_23);
        freemarkerCfg.setDirectoryForTemplateLoading(new File(TEMPLATE_FILE_PATH));
        freemarkerCfg.setDefaultEncoding("UTF-8");
        freemarkerCfg.setTemplateExceptionHandler(TemplateExceptionHandler.IGNORE_HANDLER);
    }

    /**
     * ֻ��һ�����ݿ������еı�������ȡ������ر����ݿ�����
     *
     * @return
     */
    private Set<String> getDbTableNames() {
        Set<String> dbTableNameSet = new HashSet<>();
        try (Connection connection = DriverManager.getConnection(JDBC_URL, JDBC_USERNAME, JDBC_PASSWORD);) {
            DatabaseMetaData dbMetaData = connection.getMetaData();
            ResultSet rs = dbMetaData.getTables(null, null, null, null);
            while (rs.next()) {
                final String tableName = rs.getString("TABLE_NAME");
                dbTableNameSet.add(tableName);
            }
        } catch (Exception e) {
            LOGGER.error(JDBC_URL + "::" + JDBC_USERNAME + "::" + JDBC_PASSWORD, e);
            throw new RuntimeException();//ֱ���׳�����ʱ�쳣
        }
        return dbTableNameSet;
    }

    /**
     * ����ԭTable�������Ƿ���ͨ������������ݿ��еı�����������Ҫ��ı����ú��������������
     *
     * @param newTcs         ��Table��������
     * @param dbTableNameSet ���ݿ��������
     * @param oldTc          ԭTable����
     */
    private void dealTable(Set<TableConfiguration> newTcs, Set<String> dbTableNameSet, TableConfiguration oldTc) {
        String tcTableName = oldTc.getTableName();
        // �����࣬��ͨ����Ͳ���ͨ���
        if (tcTableName.contains("*")) {
            Iterator<String> dbTableNameIter = dbTableNameSet.iterator();
            while (dbTableNameIter.hasNext()) {
                String dbTableName = dbTableNameIter.next();
                // �����б���Ϊ*�������б�����Ҫ��
                if (tcTableName.equals("*")) {
                    newTcs.add(configTable(dbTableName, null, oldTc.getGeneratedKey()));
                } else {
                    int starIndex = tcTableName.indexOf("*");
                    //��ȡǰ׺
                    String prefix = tcTableName.substring(0, starIndex);
                    //����ǰ׺Ҫ��
                    if (dbTableName.startsWith(prefix)) {
                        newTcs.add(configTable(dbTableName, prefix, oldTc.getGeneratedKey()));
                    }
                }
            }
        } else { // xml�����õľ���Ҫʹ�õı�����domain
            if (newTcs.contains(tcTableName)) {
                newTcs.add(oldTc);
            } else {
                LOGGER.warn("���ݿ��в����ڴ˱�%s", tcTableName);
            }
        }

    }

    /**
     * �����µ�TableConfiguration
     *
     * @param tableName    ԭ������
     * @param tablePrefix  ��ȥ����ǰ׺
     * @param generatedKey �������ɷ�ʽ
     * @return
     */
    private TableConfiguration configTable(String tableName, String tablePrefix, GeneratedKey generatedKey) {
        TableConfiguration tableConfiguration = new TableConfiguration(context);
        tableConfiguration.setTableName(tableName);
        tableConfiguration.setGeneratedKey(generatedKey);
        // ��ǰ׺
        if (StringUtils.isNotEmpty(tablePrefix)) {
            String domainObjectName = tableName.replaceFirst(tablePrefix, BLANK_STRING);
            tableConfiguration.setDomainObjectName(tableNameConvertUpperCamel(domainObjectName));
        }
        return tableConfiguration;
    }

    private static String tableNameConvertUpperCamel(String tableName) {
        String camel = tableNameConvertLowerCamel(tableName);
        return camel.substring(0, 1).toUpperCase() + camel.substring(1);

    }

    private static String tableNameConvertLowerCamel(String tableName) {
        StringBuilder result = new StringBuilder();
        if (tableName != null && tableName.length() > 0) {
            boolean flag = false;
            for (int i = 0; i < tableName.length(); i++) {
                char ch = tableName.charAt(i);
                if ("_".charAt(0) == ch) {
                    flag = true;
                } else {
                    if (flag) {
                        result.append(Character.toUpperCase(ch));
                        flag = false;
                    } else {
                        result.append(ch);
                    }
                }
            }
        }
        return result.toString();
    }


    private static String tableNameConvertMappingPath(String tableName) {
        return "/" + (tableName.contains("_") ? tableName.replaceAll("_", "/") : tableName);
    }

    private class TableInfo {
        String tableName;
        String tablePrefix;
        String columnPrefix;

        public TableInfo(String tableName) {
            this.tableName = tableName;
        }

        public TableInfo(String tableName, String tablePrefix, String columnPrefix) {
            this.tableName = tableName;
            this.tablePrefix = tablePrefix;
            this.columnPrefix = columnPrefix;
        }

    }

    public static void main(String[] args) throws Exception {
        CodeGenerator codeGenerator = new CodeGenerator();
        codeGenerator.generateMapper();
        codeGenerator.genServiceAndController("D:\\code\\project\\CodeGeneratorThree\\src\\main\\resources\\ssm_template_demo");
    }
}

```

##### 5. ����CodeGenerator


![���������ɳɹ�](/img/CodeGenerator/���������ɳɹ�.png.png)

�����ɳɹ���

��Ŀ���ɺ��Ŀ¼�ṹ��

![�������ɹ�Ŀ¼�ṹ](/img/CodeGenerator/�������ɹ�Ŀ¼�ṹ.png)

### ���˴������������Ժ�Ϳ��Բ�Ҫ��д��Щ�������ˣ�����ר��ȥ�о�ҵ���߼��ˡ�