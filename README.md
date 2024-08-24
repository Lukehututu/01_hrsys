# 01_hrsys

## 项目架构

![architecture](F:\project\zero-one-hrsys-1.0.0\hr-cpp\imgs\architecture.jpg)

### 各部分详细功能说明

1. **Nginx负载均衡**
   - **功能**：Nginx作为反向代理和负载均衡器，分发客户端请求到后端的API路由网关集群，以实现高可用性和负载均衡。
   - **作用**：提升系统性能和可靠性，防止单点故障。
2. **API路由网关集群**
   - **功能**：接收来自Nginx的请求，进行路由、认证、授权、聚合等操作，并将请求转发到合适的后端服务。
   - **作用**：简化客户端和后端服务的交互，增强系统的安全性和可维护性。
3. **服务注册中心**
   - **功能**：管理和维护服务实例的注册和发现，通常使用Eureka、Consul等。
   - **作用**：使服务消费者能够动态发现服务提供者，实现服务的动态扩展和负载均衡。
4. **配置中心服务集群**
   - **功能**：集中管理和分发配置，常用工具如Spring Cloud Config、Apollo等。
   - **作用**：简化配置管理，支持配置的动态更新和环境隔离。
5. **服务提供者集群（Provider）**
   - **功能**：实现具体的业务逻辑和功能，通过注册中心注册自己。
   - **作用**：提供业务功能和服务响应。
6. **服务消费者集群（Consumer）**
   - **功能**：调用服务提供者的接口，完成业务流程。
   - **作用**：协调多个服务提供者，实现业务流程。
7. **消息代理（RocketMQ）**
   - **功能**：处理异步消息传递，支持高并发、高可靠的消息队列。
   - **作用**：解耦服务，缓解服务间的依赖，提高系统的响应速度和可靠性。
8. **Docker部署**
   - **功能**：容器化部署，支持快速部署、扩展和迁移。
   - **作用**：提高开发、测试和生产环境的一致性，简化部署流程。
9. **FastDFS文件存储**
   - **功能**：分布式文件系统，存储和管理大文件。
   - **作用**：高效的文件存储和访问，支持大规模文件处理。
10. **Seata事务管理**
    - **功能**：分布式事务管理框架，确保分布式系统中的数据一致性。
    - **作用**：解决分布式系统中的事务一致性问题，支持分布式事务的提交和回滚。
11. **MySQL存储主业务数据**
    - **功能**：关系型数据库，用于存储关键业务数据。
    - **作用**：提供高可靠的数据存储和查询能力，支持复杂的业务逻辑和事务。
12. **Redis缓存数据**
    - **功能**：内存数据库，提供高性能的数据缓存和快速访问。
    - **作用**：加速数据读取，减轻数据库负载，提供快速的数据查询和处理。
13. **MongoDB存储文档类型**
    - **功能**：NoSQL数据库，适合存储文档类型的数据。
    - **作用**：提供灵活的数据模型和高扩展性，适合处理大规模和复杂的数据结构。
14. **ELK日志系统**
    - **功能**：ELK（Elasticsearch, Logstash, Kibana）用于日志收集、分析和展示。
    - **作用**：集中管理和分析日志，支持实时监控和问题排查。
15. **服务监控中心**
    - **功能**：监控系统的运行状态，通常使用Prometheus、Grafana等工具。
    - **作用**：实时监控系统性能、资源使用和服务健康状态，及时发现和解决问题。

### 数据流示例

1. **用户请求**
   - 用户通过客户端发送请求到Nginx。
   - Nginx将请求负载均衡到API路由网关集群。
2. **API网关处理**
   - API网关验证请求，进行路由和聚合。
   - API网关将请求转发到具体的服务消费者。
3. **服务调用**
   - 服务消费者通过服务注册中心发现服务提供者，并调用相关接口。
   - 服务提供者处理请求，可能需要访问MySQL、Redis、MongoDB或调用其他服务。
4. **异步处理**
   - 服务提供者通过RocketMQ发送异步消息，处理异步任务。
   - 消息消费者从RocketMQ队列中消费消息，进行进一步处理。
5. **文件存储**
   - 需要文件存储的请求通过FastDFS进行文件的存储和访问。
6. **事务管理**
   - Seata确保分布式事务的一致性，协调多个服务间的事务操作。
7. **数据缓存**
   - 频繁访问的数据存储在Redis中，以提高访问速度。
8. **日志和监控**
   - 所有的操作和请求日志通过Logstash收集，存储在Elasticsearch中，并通过Kibana进行展示和分析。
   - Prometheus和Grafana监控系统的运行状态，提供实时的性能和健康监控。

## 目录结构说明

> `arch-demo`
>
> >`conf` -- Windows平台需要的配置文件
> >
> >`controller` -- `MVC`中Controller实现，用于接收用户请求
> >
> >`service` -- 业务逻辑服务层
> >
> >`dao` -- 数据库访问层
> >
> >`domain`  -- 领域模型实体
> >
> >`public` -- 测试访问网页案例
> >
> >`Macros.h` -- 通用宏定义
> >
> >`uselib` -- 静态库使用案例
> >
> >`*.vcxproj.*` -- Windows平台项目配置文件
> >
> >`CMakeLists.txt` -- `Cmake`跨平台编译配置文件
> >
> >`Macros.h` -- 通用宏定义
> >
> >`ServerInfo.h` -- 服务器信息缓存单例
> >
> >`stdafx.h` -- 预编译标头文件
> >
> >`main.cpp` -- 程序入口
> >
> >`public.pem` -- `RSA`公钥
> >
> >`zh-dict.yaml` -- 中文词典配置

### 详解

详细解析框架中每个部分的作用

#### `controller`

在 `oatpp` 框架中，`controller` 组件主要负责处理 HTTP 请求和生成 HTTP 响应。具体来说，它定义了各种 API 端点（endpoint），这些端点对应不同的 URL 路径和 HTTP 方法（如 GET、POST 等）。每个端点都有一个处理函数，当服务器接收到对应的请求时，会调用这些处理函数来处理请求逻辑并返回响应。

1. **定义 API 路径和方法**

   控制器类中的每个函数都可以通过注解(`annotation`)指定一个 API 路径和 HTTP 方法.这些注解函数与特定的 URL 路径和方法绑定在一起

2. **处理 HTTP 请求**

   控制器类中的函数包含处理请求的逻辑.例如,解析请求参数,访问数据库,执行业务逻辑等

3. **生成 HTTP 响应**

   控制器函数在处理完请求后生成并返回 HTTP 响应.相应可以是简单的文本,JSON数据,文件等

其中`controller`层的架构

```css
controller/
    ├── sample/
    │   └── SampleController.hpp
    └── user/
    |   └── UserController.hpp
	|__ OtherComponent.hpp
	|__ Router.cpp
	|__ Router.h
	|__ SystemInterceptor.cpp
```

##### `sample`层

通常用于演示基本功能或提供样板代码.这一层的主要目的是展示如何实现特定的功能,为其他模块提供参考.它也可以用于测试某些功能的基本实现

**具体功能:**

- **示例端点(endpoint):** 提供一些简单的端点,演示如何处理 HTTP 请求和响应
- **基础逻辑:** 实现一些基础的业务逻辑,为其他模块提供参考
- **测试功能:** 可以用于测试框架或库的基本功能

##### `User`层

专门处理用户相关的功能和业务逻辑.该层的目的是实现所有与用户管理相关的功能,如用户注册,登录,认证,用户信息管理等

**具体功能:**

- **用户注册:** 实现用户注册功能,处理处理用户提交的注册信息并保存到数据库
- **用户登录:** 实现用户登录功能,验证用户凭据并生成 JWT 令牌
- **用户信息管理:** 提供用户信息的查询和更新接口
- **用户认证:** 实现JWT认证,保护需要授权访问的资源

##### 代码分析

> SampleController.h

```cpp
#pragma once

--------------------------------------------------------
#ifndef _SAMPLE_CONTROLLER_
#define _SAMPLE_CONTROLLER_
//	宏定义防止被重复包含
--------------------------------------------------------

--------------------------------------------------------
#include "domain/vo/BaseJsonVO.h"
#include "domain/query/sample/SampleQuery.h"
#include "domain/dto/sample/SampleDTO.h"
#include "domain/vo/sample/SampleVO.h"
#include "oatpp/web/mime/multipart/InMemoryDataProvider.hpp"
#include "oatpp/web/mime/multipart/FileProvider.hpp"
#include "oatpp/web/mime/multipart/Reader.hpp"
#include "oatpp/web/mime/multipart/PartList.hpp"
--------------------------------------------------------

--------------------------------------------------------
using namespace oatpp;
namespace multipart = oatpp::web::mime::multipart;

// 0 定义API控制器使用宏
#include OATPP_CODEGEN_BEGIN(ApiController) //<- Begin Codegen
// 定义命名空间和宏,以便后面使用 Oat++ 的 API 控制器功能
--------------------------------------------------------


/**
 * 示例控制器，演示基础接口的使用
 */
class SampleController : public oatpp::web::server::api::ApiController // 1 继承控制器
{
	// 2 定义控制器访问入口
	API_ACCESS_DECLARE(SampleController);
	// 3 定义接口
public:
	// 3.1 定义查询接口描述
	ENDPOINT_INFO(querySample) {
		// 定义接口标题
		info->summary = ZH_WORDS_GETTER("sample.get.summary");
		// 定义默认授权参数（可选定义，如果定义了，下面ENDPOINT里面需要加入API_HANDLER_AUTH_PARAME）
		API_DEF_ADD_AUTH();
		// 定义响应参数格式
		API_DEF_ADD_RSP_JSON_WRAPPER(SamplePageJsonVO);
		// 定义分页参数描述
		API_DEF_ADD_PAGE_PARAMS();
		// 定义其他表单参数描述
		info->queryParams.add<String>("name").description = ZH_WORDS_GETTER("sample.field.name");
		info->queryParams["name"].addExample("default", String("li ming"));
		info->queryParams["name"].required = false;
		info->queryParams.add<String>("sex").description = ZH_WORDS_GETTER("sample.field.sex");
		info->queryParams["sex"].addExample("default", String("N"));
		info->queryParams["sex"].required = false;
	}
--------------------------------------------------------
	// 3.2 定义查询接口处理
	ENDPOINT(API_M_GET, "/pimqualmajors/fetchxzzgzy", querySample, API_HANDLER_AUTH_PARAME, QUERIES(QueryParams, queryParams)) {
		// 解析查询参数
		API_HANDLER_QUERY_PARAM(userQuery, SampleQuery, queryParams);
		// 响应结果
		API_HANDLER_RESP_VO(execQuerySample(userQuery, authObject->getPayload()));
	}
    //	定义一个 GET 请求的接口 /pimqualmajors/fetchxzzgzy ,处理查询参数并调用 execQuerySample 方法处理业务逻辑
--------------------------------------------------------
    
--------------------------------------------------------
//	定义新增接口
	// 3.1 定义新增接口描述
	ENDPOINT_INFO(addSample) {
		// 定义接口标题
		info->summary = ZH_WORDS_GETTER("sample.post.summary");
		// 定义响应参数格式
		API_DEF_ADD_RSP_JSON_WRAPPER(Uint64JsonVO);
	}
	// 3.2 定义新增接口处理
	ENDPOINT(API_M_POST, "/sample", addSample, BODY_DTO(SampleDTO::Wrapper, dto)) {
		// 响应结果
		API_HANDLER_RESP_VO(execAddSample(dto));
	}
	// 3.1 定义修改接口描述
	ENDPOINT_INFO(modifySample) {
		// 定义接口标题
		info->summary = ZH_WORDS_GETTER("sample.put.summary");
		// 定义响应参数格式
		API_DEF_ADD_RSP_JSON_WRAPPER(Uint64JsonVO);
	}
	// 3.2 定义修改接口处理
	ENDPOINT(API_M_PUT, "/sample", modifySample, BODY_DTO(SampleDTO::Wrapper, dto)) {
		// 响应结果
		API_HANDLER_RESP_VO(execModifySample(dto));
	}
	// 3.1 定义删除接口描述
	ENDPOINT_INFO(removeSample) {
		// 定义接口标题
		info->summary = ZH_WORDS_GETTER("sample.delete.summary");
		// 定义响应参数格式
		API_DEF_ADD_RSP_JSON_WRAPPER(Uint64JsonVO);
	}
	// 3.2 定义删除接口处理
	ENDPOINT(API_M_DEL, "/sample", removeSample, BODY_DTO(SampleDTO::Wrapper, dto)) {
		// 响应结果
		API_HANDLER_RESP_VO(execRemoveSample(dto));
	}

	// [其他] 定义一个单文件上传接口
	ENDPOINT(API_M_POST, "/upload", uploadFile, REQUEST(std::shared_ptr<IncomingRequest>, request)) {
		/* 创建multipart容器 */
		auto multipartContainer = std::make_shared<multipart::PartList>(request->getHeaders());
		/* 创建multipart读取器 */
		multipart::Reader multipartReader(multipartContainer.get());
		/* 配置读取器读取表单字段 */
		multipartReader.setPartReader("nickname", multipart::createInMemoryPartReader(-1 /* max-data-size */));
		multipartReader.setPartReader("age", multipart::createInMemoryPartReader(-1 /* max-data-size */));
		/* 配置读取器读取文件到文件 */
		multipartReader.setPartReader("file", multipart::createFilePartReader("public/static/file/test.png"));
		/* 读取请求体中的数据 */
		request->transferBody(&multipartReader);
		/* 打印part数量 */
		OATPP_LOGD("Multipart", "parts_count=%d", multipartContainer->count());
		/* 获取表单数据 */
		auto nickname = multipartContainer->getNamedPart("nickname");
		auto age = multipartContainer->getNamedPart("age");
		/* 断言表单数据是否正确 */
		OATPP_ASSERT_HTTP(nickname, Status::CODE_400, "nickname is null");
		OATPP_ASSERT_HTTP(age, Status::CODE_400, "age is null");
		/* 打印应表单数据 */
		OATPP_LOGD("Multipart", "nickname='%s'", nickname->getPayload()->getInMemoryData()->c_str());
		OATPP_LOGD("Multipart", "age='%s'", age->getPayload()->getInMemoryData()->c_str());
		/* 获取文件部分 */
		auto filePart = multipartContainer->getNamedPart("file");
		/* 断言文件是否获取到 */
		OATPP_ASSERT_HTTP(filePart, Status::CODE_400, "file is null");
		/* 打印文件名称 */
		OATPP_LOGD("Multipart", "file='%s'", filePart->getFilename()->c_str());
		/* 响应OK */
		return createResponse(Status::CODE_200, "OK");
	}
	// [其他] 定义一个多文件上传接口
	ENDPOINT(API_M_POST, "/upload-more", uploadFileMore, REQUEST(std::shared_ptr<IncomingRequest>, request)) {
		/* 创建multipart容器 */
		auto multipartContainer = std::make_shared<multipart::PartList>(request->getHeaders());
		/* 创建multipart读取器 */
		multipart::Reader multipartReader(multipartContainer.get());
		/* 配置读取器读取文件到文件 */
		multipartReader.setPartReader("file0", multipart::createFilePartReader("public/static/file/test1.png"));
		multipartReader.setPartReader("file1", multipart::createFilePartReader("public/static/file/test2.png"));
		/* 读取请求体中的数据 */
		request->transferBody(&multipartReader);
		/* 获取文件部分 */
		auto file0 = multipartContainer->getNamedPart("file0");
		auto file1 = multipartContainer->getNamedPart("file1");
		/* 断言文件是否获取到 */
		OATPP_ASSERT_HTTP(file0, Status::CODE_400, "file0 is null");
		OATPP_ASSERT_HTTP(file1, Status::CODE_400, "file1 is null");
		/* 响应OK */
		return createResponse(Status::CODE_200, "OK");
	}
--------------------------------------------------------
//	定义了一些私有方法,用于具体处理业务逻辑,如查询,新增,修改,和删除样本数据
private:
	// 3.3 演示分页查询数据
	SamplePageJsonVO::Wrapper execQuerySample(const SampleQuery::Wrapper& query, const PayloadDTO& payload);
	// 3.3 演示新增数据
	Uint64JsonVO::Wrapper execAddSample(const SampleDTO::Wrapper& dto);
	// 3.3 演示修改数据
	Uint64JsonVO::Wrapper execModifySample(const SampleDTO::Wrapper& dto);
	// 3.3 演示删除数据
	Uint64JsonVO::Wrapper execRemoveSample(const SampleDTO::Wrapper& dto);
};
--------------------------------------------------------
// 0 取消API控制器使用宏
#include OATPP_CODEGEN_END(ApiController) //<- End Codegen
#endif // _SAMPLE_CONTROLLER_
```

> UserController.h

```cpp
#pragma once
#ifndef _USERCONTROLLER_H_
#define _USERCONTROLLER_H_
//	防止头文件被重复包含
--------------------------------------------------------
#include "oatpp-swagger/Types.hpp"
#include "domain/query/user/UserQuery.h"
#include "domain/vo/BaseJsonVO.h"
#include "domain/vo/user/UserVO.h"
#include "domain/vo/user/MenuVO.h"

using namespace oatpp;

#include OATPP_CODEGEN_BEGIN(ApiController) //<- Begin Codegen
//	引入了 Oat++ Swagger 类型定义和一些用户相关的头文件
--------------------------------------------------------
    
class UserController : public oatpp::web::server::api::ApiController
{
	// 添加访问定义	--	这个宏用于声明控制器的访问权限和声明控制器类
	API_ACCESS_DECLARE(UserController);
public:
--------------------------------------------------------    
	// 定义查询所有用户信息接口端点描述
	ENDPOINT_INFO(queryAllUser) {
		// 定义接口标题
		info->summary = ZH_WORDS_GETTER("user.query-all.summary");
		// 添加默认授权参数
		API_DEF_ADD_AUTH();
		// 定义响应参数格式
		API_DEF_ADD_RSP_JSON(UserPageJsonVO::Wrapper);
		// 定义分页参数描述
		API_DEF_ADD_PAGE_PARAMS();
		// 定义其他查询参数描述
		info->queryParams.add<String>("nickname").description = ZH_WORDS_GETTER("user.query-all.nickname");
	}
	// 定义查询所有用户信息接口端点处理
	ENDPOINT(API_M_GET, "/user/query-all", queryAllUser, API_HANDLER_AUTH_PARAME, QUERIES(QueryParams, queryParams)) {
		// 解析查询参数
		API_HANDLER_QUERY_PARAM(userQuery, UserQuery, queryParams);
		// 响应结果
		API_HANDLER_RESP_VO(executeQueryAll(userQuery));
	}

--------------------------------------------------------
	// 定义文件上传端点描述
	ENDPOINT_INFO(postFile) {
		info->summary = ZH_WORDS_GETTER("user.file.summary");
		info->addConsumes<oatpp::swagger::Binary>("application/octet-stream");
		API_DEF_ADD_RSP_JSON(StringJsonVO::Wrapper);
		info->queryParams["suffix"].description = ZH_WORDS_GETTER("user.file.suffix");
		info->queryParams["suffix"].addExample("png", String(".png"));
		info->queryParams["suffix"].addExample("jpg", String(".jpg"));
		info->queryParams["suffix"].addExample("txt", String(".txt"));
	}
	// 定义文件上传端点处理
	ENDPOINT(API_M_POST, "/user/file", postFile, BODY_STRING(String, body), QUERY(String, suffix)) {
		// 执行文件保存逻辑
		API_HANDLER_RESP_VO(executePostFile(body, suffix));
	}
--------------------------------------------------------
	// 定义查询用户菜单接口端点描述
	ENDPOINT_INFO(queryMenu) {
		// 定义接口标题
		info->summary = ZH_WORDS_GETTER("user.query-menu.summary");
		// 添加默认授权参数
		API_DEF_ADD_AUTH();
		// 定义响应参数格式
		API_DEF_ADD_RSP_JSON(MenuJsonVO::Wrapper);
	}
	// 定义查询所有用户信息接口端点处理
	ENDPOINT(API_M_GET, "/user/query-menu", queryMenu, API_HANDLER_AUTH_PARAME, QUERIES(QueryParams, queryParams)) {
		// 响应结果
		API_HANDLER_RESP_VO(executeQueryMenu(authObject->getPayload()));
	}
--------------------------------------------------------
private:
	// 查询所有
	UserPageJsonVO::Wrapper executeQueryAll(const UserQuery::Wrapper& userQuery);
	// 保存文件
	StringJsonVO::Wrapper executePostFile(const String& fileBody, const String& suffix);
	// 测试菜单
	MenuJsonVO::Wrapper executeQueryMenu(const PayloadDTO& payload);
};

#include OATPP_CODEGEN_END(ApiController) //<- End Codegen

#endif // _USERCONTROLLER_H_
```

##### 防止头文件重复编译**

此处使用了双重保障`#pragma once`和`include guard`(可以理解为引用防护)

```cpp
#pragma once
#ifndef macro_name		---- 此处是ndef
#define macro_name
//	头文件具体内容
...

#endif
```

第一次编译时`macro_name`没被定义因此条件为真,因此先`#define macro_name`,然后编译头文件内容,下一次再包含,那就先`#pragma once`有可能再去判断`#ifndef macro_name`但此时已经条件为假了,因此直接跳过中间内容.这样双重保障不会被重复编译

###### 为什么要双重防护?

对于`#pragma once`并不是所有编译器都支持(虽然现代编译器都支持),对于一个复杂的系统,可能会有兼容问题,因此需要双重防护

## 关键代码示例

### yaml文件

YAML（Yet Another Markup Language 或 YAML Ain't Markup Language）是一种人类可读的、用于表示数据的序列化格式。它被广泛用于配置文件、数据交换、应用程序设置等。YAML 设计简单明了，易于阅读和编写，同时能够表示复杂的数据结构。

#### **语法特点**

- **缩进表示层次结构**：YAML 使用缩进来表示数据的层次结构，缩进通常使用空格，而不是制表符。

- 键值对

  ：基本的 YAML 语法是通过键值对来表示数据，类似于 JSON。例如：

  ```yaml
  name: John Doe
  age: 30
  ```

- 列表

  ：列表可以通过短横线（-）来表示：

  ```yaml
  hobbies:
    - Reading
    - Hiking
    - Coding
  ```

- 嵌套结构

  ：YAML 允许嵌套的数据结构，例如嵌套的字典：

  ```yaml
  person:
    name: John Doe
    age: 30
    address:
      street: 123 Main St
      city: Hometown
  ```

####  **用途**

- **配置文件**：许多应用程序和框架使用 YAML 文件来管理配置。例如，Kubernetes 使用 YAML 文件来定义集群中的资源配置；Ansible 使用 YAML 文件定义任务和剧本。
- **数据序列化**：YAML 可以用作数据交换的格式，在某些应用程序中，它用于存储数据或在不同系统之间交换数据。
- **文档格式**：由于其可读性，YAML 也用于文档配置，例如 API 文档中的 OpenAPI 规范（Swagger）。

### `Controller`层

> `TestController.h`

```cpp
#pragma once

#ifndef _TESTCONTROLLER_H
#define _TESTCONTROLLER_H

#include "ApiHelper.h"
#include "domain/vo/BaseJsonVO.h"
#include "domain/query/PageQuery.h"

#include OATPP_CODEGEN_BEGIN(ApiController) // 0

/*
	测试控制器
*/

class TestController : public oatpp::web::server::api::ApiController { // 1

	//	2 定义控制器访问入口
	API_ACCESS_DECLARE(TestController);

public:	//	 定义接口
    
    //	都会体现在文档中
	-----------------------------------------------------------------
	//	3 定义接口描述
	ENDPOINT_INFO(queryTest) {
		//	定义接口标题
		info->summary = "test query";
		//	定义相应类型参数
		API_DEF_ADD_RSP_JSON_WRAPPER(StringJsonVO);
		//	定义分页查询参数描述
		API_DEF_ADD_PAGE_PARAMS();
	}
    ------------------------------------------------------------------
        
	//	4 定义接口端点
	ENDPOINT(API_M_GET, "/test", queryTest, QUERIES(QueryParams,qps)) {
		//	解析查询参数 （解析成领域模型对象 传递）
		API_HANDLER_QUERY_PARAM(query, PageQuery , qps);
		//	响应结果
		API_HANDLER_RESP_VO(execQueryTest(query));
	}

private://	定义接口执行函数

	//	5 定义接口的执行函数
	StringJsonVO::Wrapper execQueryTest(const PageQuery::Wrapper& query);
};


#include OATPP_CODEGEN_END(ApiController)

#endif // !_TESTCONTROLLER_H_

```

> TestController.cpp

```cpp
#include "stdafx.h"
#include "TestController.h"

StringJsonVO::Wrapper TestController::execQueryTest(const PageQuery::Wrapper& query) {
	auto vo = StringJsonVO::createShared();
	vo->success("test query success");
	return vo;
}
```

再定义完控制器后	->	将其绑定到路由中

> Router.cpp

```cpp
...
#include "test/TestController.h"
...
    
...
void Router::initRouter()
{
#ifdef HTTP_SERVER_DEMO
	createSampleRouter();
#endif

	//#TIP :系统扩展路由定义，写在这个后面
	ROUTER_SIMPLE_BIND(TestController);		//	用简单绑定宏 绑定控制器

}
...
/*	也可以在改函数中统一进行绑定,这样易于维护
#ifdef HTTP_SERVER_DEMO
void Router::createSampleRouter()
{
	// 绑定示例控制器
	ROUTER_SIMPLE_BIND(SampleController);
	// 绑定用户控制器
	ROUTER_SIMPLE_BIND(UserController);
	
	// 绑定WebSocket控制器
	router->addController(WSContorller::createShared());
}
#endif
*/
//	
```

当添加完示例控制器后,可见api文档中已经多出来了一个端点 

![image-20240813223635159](F:\project\zero-one-hrsys-1.0.0\hr-cpp\imgs\image-20240813223635159.png)

# MVC架构

## `Domain`

#### 为什么好多model都要::`Wrapper`?

Oatpp中,`wrapper`提供了一种安全,灵活的方式来管理DTO对象和其他数据类型的生命周期.`Wrapper`可以理解为Oatpp的==智能指针==,不仅能自动管理对象的内存,还能增强DTO的功能.

1. **内存管理**:
   - `Wrapper` 作为智能指针，自动管理内存分配和释放，防止内存泄漏。当 `Wrapper` 指向的对象不再被引用时，内存会自动释放。
2. **空值支持**:
   - `Wrapper` 提供了对空值的支持，允许对象为空（`nullptr`），这在处理可选字段时非常有用。它使得 DTO 字段可以区分“未设置”（`null`）和“设置为空字符串或零”（对于基本类型）。
3. **一致性与接口支持**:
   - 在 Oatpp 中，几乎所有 DTO 字段都使用 `Wrapper`，这确保了接口的一致性，并且可以使用 Oatpp 的内置功能进行 JSON 序列化、反序列化等操作。
4. **可组合性**:
   - 由于 `Wrapper` 是 Oatpp 的一种基本类型，它可以很好地与其他 Oatpp 组件（如异步操作、请求处理等）结合使用。

### 数据类型的选择

#### 对于`int`而言

有很多的int

```cpp
typedef oatpp::data::mapping::type::Int8 Int8;
typedef oatpp::data::mapping::type::UInt8 UInt8;
typedef oatpp::data::mapping::type::Int16 Int16;
typedef oatpp::data::mapping::type::UInt16 UInt16;
typedef oatpp::data::mapping::type::Int32 Int32;
typedef oatpp::data::mapping::type::UInt32 UInt32;
typedef oatpp::data::mapping::type::Int64 Int64;
```

但什么时候选择,往往取决于:

- 本身的性质,例如如果是 id 则可能很长,同时是个非负数 因此会用`UInt64`,而对于年龄来说,它基本上就是不超过100的整数,因此我们常用`Int32`,但为什么不用`Int8` ? 为什么不用`Unsigned` ? 因为往往要与系统的其他部分接口对接,要保证数据类型的一致性,因此用`Int32` 



query模型没有在api文档显示，那模型描述是写给谁看的？

## `Controller`

1. **UserController（用户控制器）**

- **职责**: 专注于处理与用户相关的操作，如用户注册、登录、用户信息管理等。
- **原因**: 用户管理通常是 Web 应用中的核心功能模块之一，需要专门的控制器来处理用户的创建、认证、权限管理等复杂的业务逻辑。将用户操作与其他操作分离，可以提高代码的可读性和维护性。

2. **SampleController（样本控制器）**

- **职责**: 处理与“样本”相关的操作，样本在你的业务中可能代表某种特定的数据对象或资源。
- **原因**: 样本管理可能是你的应用中的另一个重要功能模块。它可能涉及数据的增删改查、文件上传等操作。通过将这些操作封装在一个专门的控制器中，可以保持代码的结构化和模块化，从而更容易扩展和维护。

#### 一个接口示例

```cpp
    // 3.1 定义查询接口描述
ENDPOINT_INFO(querySample) {
    // 定义接口标题					这是yaml的引用方式 sample->get->summary
    info->summary = ZH_WORDS_GETTER("sample.get.summary");
    // 定义默认授权参数（可选定义，如果定义了，下面ENDPOINT里面需要加入API_HANDLER_AUTH_PARAME）
    API_DEF_ADD_AUTH();
    // 定义响应参数格式
    API_DEF_ADD_RSP_JSON_WRAPPER(SamplePageJsonVO);
    // 定义分页参数描述
    API_DEF_ADD_PAGE_PARAMS();
    // 定义其他表单参数描述
    info->queryParams.add<String>("name").description = ZH_WORDS_GETTER("sample.field.name");
    info->queryParams["name"].addExample("default", String("li ming"));
    info->queryParams["name"].required = false;
    info->queryParams.add<String>("sex").description = ZH_WORDS_GETTER("sample.field.sex");
    info->queryParams["sex"].addExample("default", String("N"));
    info->queryParams["sex"].required = false;
}
// 3.2 定义查询接口处理
/*
*		GET 方法(封装过的)
*		"/pimqualmajors/fetchxzzgzy" 该端点的URL
*		querySample 该端点的处理函数的名称
*		API_HANDLER_AUTH_PARAME	用于处理授权参数的宏 确保请求用户具有执行该操作的权限
*		QUERIES(QueryParams, queryParams)	Oatpp特有的宏,指定该缎带你将接受查询参数 并将其解析为一个\		
*											QueryParams类型的变量`queryParams`
*/		

ENDPOINT(API_M_GET, "/pimqualmajors/fetchxzzgzy", querySample, API_HANDLER_AUTH_PARAME, QUERIES(QueryParams, queryParams)) {
    // 解析查询参数
    //	将queryParams转化为SampleQuery类型的`userQuery`对象(Sample是定义查询条件的DTO)
    API_HANDLER_QUERY_PARAM(userQuery, SampleQuery, queryParams);
    // 响应结果 用于处理和返回API响应
    //	调用了execQuerySample函数 将userQuery和authObject->getPayload()参数传进去
    //						该函数是实际处理查询的函数,会根据查询条件和授权对象的有效负载进行操作并返回相应的数据
    API_HANDLER_RESP_VO(execQuerySample(userQuery, authObject->getPayload()));
}
```

> execQuerySample()

```cpp
SamplePageJsonVO::Wrapper SampleController::execQuerySample(const SampleQuery::Wrapper& query, const PayloadDTO& payload)
{
	// 定义一个Service -- 用来传递到 Service 层
	SampleService service;
	// 查询数据	-- listAll方法返回查询结果(SamplePageDTO::Wrapper 对象)
	auto result = service.listAll(query);
	// 响应结果
	auto jvo = SamplePageJsonVO::createShared();
    // 通过 success方法 生成响应
	jvo->success(result);
	return jvo;
}
```



![image-20240814151756144](C:\Users\Luk1\AppData\Roaming\Typora\typora-user-images\image-20240814151756144.png)

#### 实际接口

> UserController.h

```cpp
//	定义查询所有用户信息接口端点描述
ENDPOINT_INFO(queryAllUser) {
    //	定义接口标题
    info->summary = ZH_WORDS_GETTER("user.query-all.summary");
    //	添加默认授权参数
    API_DEF_ADD_AUTH();
    //	定义响应参数格式
    API_DEF_ADD_RSP_JSON(UserPageJsonVO::Wrapper);
    //	定义其他查询参数描述
    info->queryParams.add<String>("nickname").description = ZH_WORDS_GETTER("user.query-all.nickname");
}
//	定义查询所有用户信息接口端点处理
ENDPOINT(API_M_GET, "/user/query-all", queryAllUser, API_HANDLER_AUTH_PARAME, QUERIES(QueryParams, queryParams)) {
    //	解析查询参数
    API_HANDLER_QUERY_PARAM(userQuery, UserQuery, queryParams);
    //	响应结果
    API_HANDLER_RESP_VO(executeQueryAll(userQuery));
}
```

> UserController.cpp

```cpp
//	查询所有
UserPageJsonVO::Wrapper UserController::executeQueryAll(const UserQuery::Wrapper& userQuery) {
	//	定义一个JsonVO对象
	auto vo = UserPageJsonVO::createShared();
	//	定义一个分页对象
	auto page = UserPageDTO::createShared();
	page->pageIndex = userQuery->pageIndex;
	page->pageSize = userQuery->pageSize;
	page->total = 20;
	page->calcPages();

	//	模拟计算分页数据
	int64_t start = (page->pageIndex.getValue(1) - 1) * page->pageSize.getValue(1);
	int64_t end = start + page->pageSize.getValue(1);
	//	边界值处理
	if (start >= page->total.getValue(0)) end = page->total.getValue(0);
	//	循环生成测试数据
	for (int64_t i = start; i < end; i++) {
		auto user = UserDTO::createShared();
		user->nickname = userQuery->nickname;
		user->age = (uint32_t)(i + 1) * 10;
		user->idCard = "12345678901234567" + oatpp::utils::conversion::uint64ToStdStr(i);
		page->addData(user);
	}
	//	将操作标记为suc并将page数据附加在其中
	vo->success(page);
	return vo;
}
```

**初始化对象:**

- 创建了一个 `UserPageJsonVO` 对象来存储结果。
- 初始化了一个 `UserPageDTO` 对象来处理分页相关的细节。

**分页设置:**

- `pageIndex` 和 `pageSize` 是从 `userQuery` 参数中获取的。
- `total`（总记录数）被硬编码为 20。
- 调用了 `calcPages()` 方法，根据 `total`、`pageIndex` 和 `pageSize` 计算总页数。

**分页逻辑:**

- `start` 是基于当前页码计算出的记录起始索引。
- `end` 是结束索引，并经过调整以确保不超过总记录数。
- 循环从 `start` 到 `end` 生成模拟用户数据。

**生成模拟数据:**

- 对于每个索引，创建一个 

  ```
  UserDTO
  ```

   对象，并填充模拟数据：

  - `nickname` 来自于 `userQuery`。
  - `age` 通过 `(i + 1) * 10` 计算得出。
  - `idCard` 是一个带有唯一标识符的模拟字符串。

**构建响应:**

- 生成的用户数据被添加到 `page` 对象中。
- 调用了 `vo` 对象的 `success()` 方法，将操作标记为成功并附加 `page` 数据。
- 最后返回 `vo` 对象。



## `Service`

### TreeMenuMapper.h

```cpp
#pragma once
#ifndef _TREEMENU_MAPPER_H_
#define _TREEMENU_MAPPER_H_

#include "tree/TreeNodeMapper.h"
#include "domain/do/user/MenuDO.h"
#include "domain/dto/user/MenuDTO.h"

//	演示菜单数据字段匹配实现

class TreeMenuMapper : public TreeNodeMapper<MenuDO> {
public:
	shared_ptr<TreeNode> objectMapper(MenuDO* source) const override {
		//	创建结果数据对象
		auto res = make_shared<MenuDTO>();
		//	计算层级结构属性映射
		res->_id(source->getId());
		res->_pid(source->getParentId());
		//	扩展属性映射
		res->text = source->getText();
		res->icon = source->getIcon();
		res->href = source->getHref();
		return res;
	}
};

#endif // !_TREEMENU_MAPPER_H_
```

1. **TreeMenuMapper 类:**
   - `TreeMenuMapper` 继承自 `TreeNodeMapper<MenuDO>`，并重写了 `objectMapper` 方法。
   - `objectMapper` 方法用于将 `MenuDO` 对象映射到 `MenuDTO` 对象。
2. **objectMapper 方法实现:**
   - `objectMapper` 方法接收一个指向 `MenuDO` 对象的指针 `source`，并返回一个指向 `TreeNode`（即 `MenuDTO`）的共享指针。
   - 通过 `make_shared<MenuDTO>()` 创建一个 `MenuDTO` 对象，并将其赋值给 `res`。
   - 映射层级结构属性：
     - `res->_id(source->getId())` 将 `source` 的 ID 映射到 `MenuDTO` 的 `_id` 属性。
     - `res->_pid(source->getParentId())` 将 `source` 的父 ID 映射到 `MenuDTO` 的 `_pid` 属性。
   - 映射扩展属性：
     - 将 `source` 的 `text`、`icon` 和 `href` 属性分别映射到 `MenuDTO` 对应的属性中。
3. **返回结果:**
   - 最后返回 `res`，即完成映射后的 `MenuDTO` 对象。

**注意事项**

- 如果在扩展映射逻辑时有更多的属性需要处理，可以在 `objectMapper` 方法中继续添加相应的映射代码。
- 确保在 `MenuDO` 和 `MenuDTO` 中定义的属性名和类型匹配。

## `DAO`

### SampleDAO.h

```cpp
class SampleDAO :public BaseDAO {
public:
	//	统计数据条数
	uint64_t count(const SampleQuery::Wrapper& query);
};
```

SampleDAO.cpp

```cpp
//	定义条件解析宏 ，减少重复代码
#define SAMPLE_TERAM_PARSE(query, sql)  \
SqlParams params; \
sql<<" WHERE 1=1"; \
if (query->name) { \
		sql << " AND `name`=?"; \
		SQLPARAMS_PUSH(params, "s", std::string, query->name.getValue("")); \
} \
if (query->sex) { \
		sql << " AND sex=?"; \
		SQLPARAMS_PUSH(params, "s", std::string, query->sex.getValue("")); \
} \
if (query->age) { \
		sql << " AND age=?"; \
		SQLPARAMS_PUSH(params, "i", int, query->age.getValue(0)); \
}

/*
SAMPLE_TERAM_PARSE: 这是一个用于条件解析的宏，生成 SQL 查询的 WHERE 子句并收集查询参数。
SqlParams params;: 初始化 SQL 参数对象。
sql << " WHERE 1=1";: 在 SQL 查询中添加一个默认的 WHERE 子句，方便后续条件的拼接。
if (query->name): 如果 query 中的 name 字段有值，则将对应的条件添加到 SQL 语句中，并将参数推入 params。
SQLPARAMS_PUSH: 将查询条件的值推入参数列表 params 中。
*/

uint64_t count(const SampleQuery::Wrapper & query) {
	stringstream sql;
	sql << "SELECT COUNT(*) FROM sample";
	SAMPLE_TERAM_PARSE(query, sql);
	string sqlStr = sql.str();
	return sqlSession->executeQueryNumerical(sqlStr, params);
}
/*
步骤:
使用 stringstream 对象 sql 构建 SQL 查询语句，首先添加 SELECT COUNT(*) FROM sample。
通过 SAMPLE_TERAM_PARSE 宏添加查询条件并收集 SQL 参数。
将最终构建的 SQL 查询字符串存储在 sqlStr 中。
调用 sqlSession->executeQueryNumerical(sqlStr, params) 执行查询并返回结果，即满足条件的记录总数。
*/
```

## 数据流动过程详述

> 前端发送用户注册请求，后端接收请求后，经过各层处理和领域模型转换，然后返回注册成功的用户信息。

### 端口选择
假设服务器监听的端口为 **8080**。

### 模拟的数据
- **前端发送的数据**:
  
  ```json
  {
    "username": "john_doe",
    "password": "securepassword123",
    "email": "john.doe@example.com"
  }
  ```

### 1. **前端发送请求**
前端通过 HTTP POST 请求将注册信息发送到 `/api/user/register` 路径，服务器监听端口 `8080`。

```http
POST /api/user/register HTTP/1.1
Host: localhost:8080
Content-Type: application/json

{
  "username": "john_doe",
  "password": "securepassword123",
  "email": "john.doe@example.com"
}
```

### 2. **后端接收请求 - Controller 层**
后端的 `UserController` 处理这个请求：

```cpp
#include "UserController.h"
#include "UserService.h"

class UserController : public oatpp::web::server::api::ApiController {
public:
    UserController(OATPP_COMPONENT(std::shared_ptr<ObjectMapper>, objectMapper))
        : oatpp::web::server::api::ApiController(objectMapper) {}

    ENDPOINT("POST", "/api/user/register", registerUser,
             BODY_DTO(UserRegisterDTO::Wrapper, userDto)) {

        auto user = UserService::registerUser(userDto);
        return createDtoResponse(Status::CODE_200, user);
    }
};
```

### 3. **Service 层处理业务逻辑**
`UserService` 负责注册逻辑，将数据传递给 DAO 层进行持久化。

```cpp
#include "UserService.h"
#include "SampleDAO.h"
#include "UserMapper.h"

class UserService {
public:
    static UserDTO::Wrapper registerUser(const UserRegisterDTO::Wrapper& userDto) {
        // 转换为领域模型
        auto userDO = UserMapper::toDomainObject(userDto);

        // 将用户信息保存到数据库
        SampleDAO::saveUser(userDO);

        // 转换为 DTO 返回
        return UserMapper::toDTO(userDO);
    }
};
```

### 4. **DAO 层进行数据持久化**
`SampleDAO` 将用户信息保存到数据库。

```cpp
#include "SampleDAO.h"
#include "UserDO.h"

class SampleDAO {
public:
    static void saveUser(const UserDO::Wrapper& userDO) {
        std::string sql = "INSERT INTO users (username, password, email) VALUES (?, ?, ?)";
        SqlParams params;
        SQLPARAMS_PUSH(params, "s", std::string, userDO->getUsername());
        SQLPARAMS_PUSH(params, "s", std::string, userDO->getPassword());
        SQLPARAMS_PUSH(params, "s", std::string, userDO->getEmail());

        sqlSession->executeUpdate(sql, params);
    }
};
```

### 5. **领域模型转换 - DTO 到 DO**
`UserMapper` 负责在不同模型之间的转换。

```cpp
#include "UserMapper.h"
#include "UserDTO.h"
#include "UserDO.h"

class UserMapper {
public:
    static UserDO::Wrapper toDomainObject(const UserRegisterDTO::Wrapper& dto) {
        auto userDO = UserDO::createShared();
        userDO->setUsername(dto->username);
        userDO->setPassword(dto->password);
        userDO->setEmail(dto->email);
        return userDO;
    }

    static UserDTO::Wrapper toDTO(const UserDO::Wrapper& do) {
        auto userDto = UserDTO::createShared();
        userDto->username = do->getUsername();
        userDto->email = do->getEmail();
        return userDto;
    }
};
```

### 6. **数据库领域对象 - UserDO**
`UserDO` 是领域对象，代表数据库中的用户数据。

```cpp
#include "UserDO.h"

class UserDO : public oatpp::DTO {
    DTO_INIT(UserDO, DTO)

    DTO_FIELD(String, username);
    DTO_FIELD(String, password);
    DTO_FIELD(String, email);

public:
    void setUsername(const String& value) { username = value; }
    void setPassword(const String& value) { password = value; }
    void setEmail(const String& value) { email = value; }
};
```

### 7. **前端返回响应 - DTO 层**
后端处理完成后，将注册成功的用户信息返回给前端。

```json
{
  "username": "john_doe",
  "email": "john.doe@example.com"
}
```

### 8. **总结流程**
- **前端** 发送注册请求。
- **Controller 层** 接收请求并调用 Service 层。
- **Service 层** 处理业务逻辑，并将 DTO 转换为领域对象 DO。
- **DAO 层** 将 DO 保存到数据库中。
- **Service 层** 再将 DO 转换为 DTO 并返回给 Controller。
- **Controller 层** 返回响应给前端。

这个过程展示了一个完整的数据流，从前端到后端再返回前端，涵盖了不同层之间的数据转换和交互。

# 相关技术

## 文件存储

在本次项目中,文件存储在了`FastDFS`服务器中,采用`Nginx`代理访问

### Docker部署FastDFS

- 先部署FastDFS服务

1. 准备`/root/dfs`路径,构建`/root/dfs/docker/dockerfile_network`目录(将应用部署文件夹中的`docker`文件夹拉到该路径下)

> DockerFile如下

```dockerfile
# centos 7
FROM centos:7
# 添加配置文件
ADD conf/client.conf /etc/fdfs/
ADD conf/http.conf /etc/fdfs/
ADD conf/mime.types /etc/fdfs/
ADD conf/storage.conf /etc/fdfs/
ADD conf/tracker.conf /etc/fdfs/
ADD fastdfs.sh /home
ADD conf/nginx.conf /etc/fdfs/
ADD conf/mod_fastdfs.conf /etc/fdfs

# run

# 替换 CentOS 7 的镜像源为阿里云
RUN sed -i 's|^mirrorlist=|#mirrorlist=|g' /etc/yum.repos.d/CentOS-Base.repo && \
    sed -i 's|^#baseurl=http://mirror.centos.org|baseurl=http://mirrors.aliyun.com|g' /etc/yum.repos.d/CentOS-Base.repo && \
    yum clean all && yum makecache
# install packages
RUN yum install git gcc gcc-c++ make automake autoconf libtool pcre pcre-devel zlib zlib-devel openssl-devel wget vim -y
# git clone libfastcommon / libserverframe / fastdfs / fastdfs-nginx-module
RUN cd /usr/local/src \
  && git clone https://gitee.com/fastdfs100/libfastcommon.git \
  && git clone https://gitee.com/fastdfs100/libserverframe.git \
  && git clone https://gitee.com/fastdfs100/fastdfs.git \
  && git clone https://gitee.com/fastdfs100/fastdfs-nginx-module.git \
  && pwd && ls
# build libfastcommon / libserverframe / fastdfs
RUN mkdir /home/dfs \
  && cd /usr/local/src  \
  && pwd && ls \
  && cd libfastcommon/   \
  && ./make.sh && ./make.sh install  \
  && cd ../  \
  && cd libserverframe/   \
  && ./make.sh && ./make.sh install  \
  && cd ../  \
  && cd fastdfs/   \
  && ./make.sh && ./make.sh install
# download nginx and build with fastdfs-nginx-module
# 推荐 NGINX 版本:
# NGINX_VERSION=1.16.1
# NGINX_VERSION=1.17.10
# NGINX_VERSION=1.18.0
# NGINX_VERSION=1.19.10
# NGINX_VERSION=1.20.2
# NGINX_VERSION=1.21.6
# NGINX_VERSION=1.22.1
# NGINX_VERSION=1.23.3
# 可在 docker build 命令中指定使用的 nginx 版本, 例如:
# docker build --build-arg NGINX_VERSION="1.16.1" -t happyfish100/fastdfs:latest -t happyfish100/fastdfs:6.09.01 .
# docker build --build-arg NGINX_VERSION="1.19.10" -t happyfish100/fastdfs:latest -t happyfish100/fastdfs:6.09.02 .
# docker build --build-arg NGINX_VERSION="1.23.3" -t happyfish100/fastdfs:latest -t happyfish100/fastdfs:6.09.03 .
ARG NGINX_VERSION=1.16.1
RUN cd /usr/local/src \
  && NGINX_PACKAGE=nginx-${NGINX_VERSION} \
  && NGINX_FILE=${NGINX_PACKAGE}.tar.gz \
  && wget http://nginx.org/download/${NGINX_FILE} \ 
  && tar -zxvf ${NGINX_FILE} \
  && pwd && ls \
  && cd /usr/local/src \
  && cd ${NGINX_PACKAGE}/  \
  && ./configure --add-module=/usr/local/src/fastdfs-nginx-module/src/   \
  && make && make install  \
  && chmod +x /home/fastdfs.sh

# 原来的 RUN 语句太复杂, 不利于 docker build 时使用多阶段构建缓存
# RUN yum install git gcc gcc-c++ make automake autoconf libtool pcre pcre-devel zlib zlib-devel openssl-devel wget vim -y \
#   &&    NGINX_VERSION=1.19.9 \
#   &&    NGINX_PACKAGE=nginx-${NGINX_VERSION} \
#   &&    NGINX_FILE=${NGINX_PACKAGE}.tar.gz \
#   &&    cd /usr/local/src  \
#   &&    git clone https://gitee.com/fastdfs100/libfastcommon.git \
#   &&    git clone https://gitee.com/fastdfs100/libserverframe.git \
#   &&    git clone https://gitee.com/fastdfs100/fastdfs.git \
#   &&    git clone https://gitee.com/fastdfs100/fastdfs-nginx-module.git \
#   &&    wget http://nginx.org/download/${NGINX_FILE}    \
#   &&    tar -zxvf ${NGINX_FILE}    \
#   &&    mkdir /home/dfs   \
#   &&    cd /usr/local/src/  \
#   &&    cd libfastcommon/   \
#   &&    ./make.sh && ./make.sh install  \
#   &&    cd ../  \
#   &&    cd libserverframe/   \
#   &&    ./make.sh && ./make.sh install  \
#   &&    cd ../  \
#   &&    cd fastdfs/   \
#   &&    ./make.sh && ./make.sh install  \
#   &&    cd ../  \
#   &&    cd ${NGINX_PACKAGE}/  \
#   &&    ./configure --add-module=/usr/local/src/fastdfs-nginx-module/src/   \
#   &&    make && make install  \
#   &&    chmod +x /home/fastdfs.sh

RUN ln -s /usr/local/src/fastdfs/init.d/fdfs_trackerd /etc/init.d/fdfs_trackerd \
  && ln -s /usr/local/src/fastdfs/init.d/fdfs_storaged /etc/init.d/fdfs_storaged 

# export config
VOLUME /etc/fdfs

EXPOSE 22122 23000 8888 80
ENTRYPOINT ["/home/fastdfs.sh"]
```

主要就是按照官方文档,配置`Tracker`,`stroage`和`mime`,以及配置好nginx的FastDFS模块

2. **构建镜像**

   ```bash
   cd /root/dfs/docker/dockerfile_network/
   docker build -f ./Dockerfile -t luke/dfs .
   ```

3. 创建容器

   ```bash
   docker run -d \
   -e FASTDFS_IPADDR=192.168.136.132 \
   --net=host \
   --name fast-dfs \
   -v /home/dfs/:/home/dfs/ \
   luke/dfs
   ```

4. 开放端口

   ```bash
   #开放端口
   firewall-cmd --add-port 8888/tcp --add-port 22122/tcp --add-port 23000/tcp --
   permanent
   #重新加载防火墙
   firewall-cmd --reload
   ```

### 测试FastDFS

> TestFastDFS.h

```cpp
#pragma once
#ifndef _TEST_FASTDFS_H_
#define _TEST_FASTDFS_H_

class TestFastDFS {
public:
	static void testDFS();
};

#endif // !_TEST_FASTDFS_H_
```

> TestFastDFS.cpp

```cpp
#include "stdafx.h"
#include "TestFastDFS.h"
#include <iostream>
#include "FastDfsClient.h"


void TestFastDFS::testDFS()
{
#ifdef LINUX
	//定义客户端对象
	FastDfsClient client("conf/client.conf");
#else
	//定义客户端对象
	FastDfsClient client("192.168.136.132");
#endif
	string fileName = "../arch-demo/public/test.html";
	//测试上传
	std::string fieldName = client.uploadFile(fileName);
	std::cout << "upload fieldname is : " << fieldName << std::endl;
	//测试下载
	if (!fieldName.empty())
	{
		std::string path = "./public/fastdfs";
		fileName = client.downloadFile(fieldName, &path);
		std::cout << "download savepath is : " << fileName << std::endl;
	}
	//测试删除文件
	if (!fieldName.empty())
	{
		std::cout << "delete file result is : " << client.deleteFile(fieldName) << std::endl;
	}
}
```

1. 先注释删除文件的逻辑,来测试下载的逻辑

   

2. 再注释掉测试下载的逻辑,来测试删除文件的逻辑

## 报表

### 静态库连接

excel的静态库 -> `xlntd.lib`(debug模式下的) , `xlnt.lib`(release模式下)

在链接器的输入选项中添加

### 测试代码

> TestExcel.cpp

```cpp
//	注意：为了保证再Linux平台不乱码，需要保证本源码文件的编码为 UTF8 BOM 编码格式 即带签名的模式
void TestExcel::testExcel() {

	//	创建测试数据
	vector<vector<string>> data;
	stringstream ss;
	for (int i = 1; i <= 10; i++) {
		vector<string> row;
		for (int j = 1; j <= 5; j++) {
			ss.clear();
			//	注意： 因为xlnt 不能存储非utf8编码的字符，所以中文字需要转换编码
			ss
				<< CharsetConvertHepler::ansiToUtf8("单元格坐标：（") << i
				<< CharsetConvertHepler::ansiToUtf8(",") << j << ")";
			row.push_back(ss.str());
			ss.str("");
		}
		data.push_back(row);
	}

	//	定义保存数据位置和页签名称
	//	注意：文件名称和文件路径不能出现中文
	string fileName = "./public/excel/1.xlsx";
	//	注意：因为xlnt不能存储非utf8编码的字符，所以中文字需要转换编码
	string sheetName = CharsetConvertHepler::ansiToUtf8("数据表1");

	//	保存到文件
	ExcelComponent excel;
	excel.writeVectorToFile(fileName, sheetName, data);

	//	从文件中读取 -- 此时从文件读出的就是utf8,但如果要在控制台打印就要转回ansi(控制台编码集太久了不支持)
	auto readData = excel.readIntoVector(fileName, sheetName);
	for (auto row : readData) {
		for (auto cellVal : row) {
			/*注意，这里使用了编码转换，目的是为了在控制台打印不显示乱码，如果是将数据写入数据库，
			那就不需要转换编码，从文件中读出来是什么数据就写入什么数据*/
			cout << CharsetConvertHepler::utf8ToAnsi(cellVal);
			cout << CharsetConvertHepler::utf8ToAnsi(",");
		}
		cout << endl;
	}


	//	测试 创建 第二个页签
	sheetName = CharsetConvertHepler::ansiToUtf8("数据表2");
	excel.writeVectorToFile(fileName, sheetName, data);

	//	测试 覆盖 第一个页签
	sheetName = CharsetConvertHepler::ansiToUtf8("数据表1");
	data.insert(data.begin(), {
		CharsetConvertHepler::ansiToUtf8("表头1"),
		CharsetConvertHepler::ansiToUtf8("表头2"),
		CharsetConvertHepler::ansiToUtf8("表头3"),
		CharsetConvertHepler::ansiToUtf8("表头4"),
		CharsetConvertHepler::ansiToUtf8("表头5")
		});
	excel.writeVectorToFile(fileName, sheetName, data);
}
```

![QQ_1724210399098](C:\Users\Luk1\AppData\Local\Temp\QQ_1724210399098.png)

#### 什么时候转码,转成什么码

一般要存进excel中就统一转成`utf8`因为`utf8`兼容性更好,可以保存多种语言的字符.但如果要在控制台打印就必须转回`ANSI`编码,这是控制台的编码集

- **UTF-8**：是一种变长的字符编码，能够表示所有 Unicode 字符集的字符，包括中文字符。UTF-8 是目前互联网上最常用的编码方式，因为它兼容 ASCII 编码，并且对中文字符等非 ASCII 字符的支持良好。

- **ANSI**：是一种较老的编码方式，通常指 Windows 系统中使用的编码（如 CP-1252），它只能表示有限的字符集，主要是英文和一些其他西欧语言字符。对于中文字符，ANSI 编码不够全面，通常需要使用 UTF-8 或其他更现代的编码方式。

### 报表的前后端交互

#### 导入流程

1. 将表格保存到应用服务磁盘的临时文件目录
2. 使用excel组件从磁盘中将其读到内存中
3. 逐行解析数据，构建成对应的DTO或DO
4. 保存到数据库中，注意此处是批量操作，在service中要开启事务
5. 保存成功后删除临时目录的报表(磁盘中的)
6. 保存响应结果

#### 导出流程

(有相应的数据查询条件)

1. 验证查询条件
2. 根据条件获取数据
3. 将数据保存到excel文件中,并保存到磁盘的临时目录
4. 上传报表到FastDFS中
5. 下发文件下载地址

## 熔断限流

本项目使用了`Sentinel`(alibaba的分布式系统的流量防卫兵)来进行流量控制(但`Sentinel`是java部分的集成在`Spring Cloud`中的),

### 熔断 (Circuit Breaker)

熔断器(Circuit Breaker)是一种保护机制,防止系统中的某一部分故障扩散到整个系统.

- **工作原理:** 
  1. **关闭状态(closed)**: 正常状态,所有请求都被允许通过,系统会不断监控服务的健康状况
  2. **打开状态(open)** : 当系统检测到服务的失败率超过预设的阈值时,熔断器会进入打开状态,所有对该服务的请求都会被立刻拒绝.这样可以避免服务继续接受请求,从而减轻服务的压力,给予其恢复时间
  3. **半开状态(half open)**: 在一定时间后,熔断器会进入半开状态,允许部分请求通过,以测试服务是否已经恢复.如果测试通过,熔断器会重新进入关闭状态,如果任然失败,会再次进入打开状态

- **目的和效果:**
  - 防止服务器雪崩: 通过阻止对故障服务的请求,避免故障扩散到其他正常服务
  - 提高系统的可靠性: 通过检测和隔离故障,系统可以继续运行而不是完全崩溃
  - 给服务恢复时间: 当服务恢复正常后,熔断器会允许部分请求通过,帮助服务逐步恢复

### 限流(Rate Limiting)

**限流**是控制系统中请求处理速率的技术，目的是防止系统因为过多的请求而过载。限流可以通过多种策略实现，比如基于时间窗口的限流、漏桶算法、令牌桶算法等。

- **常见限流算法**

  1. **固定窗口计数器（Fixed Window Counter）**：将时间划分为固定长度的窗口（如每分钟），计算每个窗口内的请求数量。如果请求数量超过限制，拒绝新的请求。

  2. **滑动窗口计数器（Sliding Window Counter）**：对时间窗口进行滑动计算，比固定窗口计数器更精确，能够动态调整请求速率。

  3. **令牌桶（Token Bucket）**：允许突发请求，但在请求流量过高时限制请求速率。请求需要从令牌桶中取令牌，桶中令牌的生成速率限制了请求速率。

  4. **漏桶（Leaky Bucket）**：处理请求流量的平滑算法，将请求排队，然后按照固定速率处理请求。

- **目的和效果**

  - **防止系统过载**：限制系统接受的请求数量，以避免过多的请求导致系统崩溃或性能下降。

  - **提供公平性**：通过限流机制，确保系统资源公平分配给所有请求。

  - **保障服务质量**：防止某一用户或服务滥用资源，影响其他用户的体验。

### 熔断与限流的结合

在实际应用中，熔断和限流通常一起使用，以提供综合的系统保护措施。例如：

- **限流**可以防止请求量过大导致系统过载，从而减少系统进入熔断状态的频率。
- **熔断**则在限流机制失效或系统异常时，提供额外的保护，防止系统进一步崩溃。

## 声明式服务



## WebSocket

**连接WebSocket的静态库**

```sh
# oatpp websocket
oatpp-websocket.lib (Debug 和 Release都是这个库)
```

**在预处理中定义宏 `HTTP_SERVER_DEMO`**

### ![QQ_1724301185970](C:\Users\Luk1\AppData\Local\Temp\QQ_1724301185970.png)基本架构

```bash
userlib
|
|_ws
| |_WSController.h				---	封装了WebSocket的相关测试路由
| |_WSInstanceListener.cpp			
| |_WSInstanceListener.h		---	该类用于监听连接的 建立 和 断开
| |_WSListener.cpp
| |_WSListener.h				---	该类用于监听客户端发送的信息
```

### 代码详解

#### WSListen

> WSListener.h

```cpp
#pragma once
#ifdef HTTP_SERVER_DEMO
#ifndef _WSLISTENER_H_
#define _WSLISTENER_H_
#include "oatpp-websocket/WebSocket.hpp"
#include "oatpp-websocket/ConnectionHandler.hpp"
#include <map>

/**
 * WebSocket侦听器,侦听传入的WebSocket事件
 */
class WSListener : public oatpp::websocket::WebSocket::Listener
{
private:
    
   	//	是一个静态常量字符指针，用于表示日志输出的标签。通常在调试和日志记录时使用，方便定位输出信息的来源
	static constexpr const char* TAG = "Server_WSListener";
	// 消息缓冲区 -- 用于暂存从WebSocket接收道德消息数据
	oatpp::data::stream::BufferOutputStream m_messageBuffer;
	// 用户ID -- 用于存储当前连接WebSocket的用户ID。每个 WebSocket 连接通常对应一个唯一的用户ID
	std::string id;
	// 加入聊天室用户列表 用于维护一个聊天室中的所有WebSocket连接。key是id，value是对应的WebSOcket指针
	std::map<std::string, const WebSocket*>* conn_pool;
public:
	// 获取ID -- 简单的getter方法
	const std::string& getId();
	// 构造初始化
	WSListener(std::string id, std::map<std::string, const WebSocket*>* conn_pool);
	// 在ping帧上调用	---	当收到WebSocket Ping帧时调用,Ping帧通常用于保持连接的活跃状态,服务器在收到Ping帧后可以发送一个Pong响应
	void onPing(const WebSocket& socket, const oatpp::String& message) override;
	// 在pong帧上调用	--- Pong帧通常是对于Ping帧的响应,用于确认连接任然活跃
	void onPong(const WebSocket& socket, const oatpp::String& message) override;
	// 在close帧上调用	---	当WebSocket关闭连接时调用,可用来进行清理操作,比如从连接池中移除该连接,或者记录连接关闭的原因和状态码
	void onClose(const WebSocket& socket, v_uint16 code, const oatpp::String& message) override;
	// 在每个消息帧上调用。最后一条消息将再次调用，size等于0以指定消息结束
	void readMessage(const WebSocket& socket, v_uint8 opcode, p_char8 data, oatpp::v_io_size size) override;
};

#endif // !_WSLISTENER_H_

#endif // HTTP_SERVER_DEMO
```

> WSListener.cpp

```cpp
#include "stdafx.h"

#include "WSListener.h"
#include "StringUtil.h"

//	定义一个锁
std::mutex listener_mutex;


// 获取ID
const std::string& WSListener::getId() {
	return this->id;
}
// 构造初始化
WSListener::WSListener(std::string id, std::map<std::string, const WebSocket*>* conn_pool) {
	this->id = id;
	this->conn_pool = conn_pool;
}
// 在ping帧上调用
void WSListener::onPing(const WebSocket& socket, const oatpp::String& message) {
	//	使用该宏输出日志信息,标记为onPing
    OATPP_LOGD(TAG, "onPing");
    //	立即发送pong帧作为响应
	socket.sendPong(message);
}
// 在pong帧上调用
void WSListener::onPong(const WebSocket& socket, const oatpp::String& message)  {
    //	当接收到WebSocket的pong帧时调用,记录日志
	OATPP_LOGD(TAG, "onPong");
}
// 在close帧上调用
void WSListener::onClose(const WebSocket& socket, v_uint16 code, const oatpp::String& message) {
	//	当WebSocket关闭连接时调用,记录关闭的状态码和消息
	OATPP_LOGD(TAG, "onClose code=%d", code);
}

// 在每个消息帧上调用。最后一条消息将再次调用，size等于0以指定消息结束
void WSListener::readMessage(const WebSocket& socket, v_uint8 opcode, p_char8 data, oatpp::v_io_size size) {
	//	message transfer finished
	if (size == 0) {
		//	获取消息数据
        //	从缓冲区中提取整个消息
		auto wholeMessage = m_messageBuffer.toString().getValue("");
        //	将缓冲区清零
		m_messageBuffer.setCurrentPosition(0);
        //	记录日志,记录收到的消息
		OATPP_LOGD(TAG, "onMessage message=%s", wholeMessage.c_str());
		//	解析消息 => ID::消息内容  -->消息结构 
		std::vector<std::string> msgs = StringUtil::split(wholeMessage.c_str(), "::");
		//	群发消息ID=all表示群发
		if ("all" == msgs[0]) {
			std::lock_guard<std::mutex> guard(listener_mutex);
			for (auto one : *conn_pool) {
				//	排除自己
				if (one.second == &socket) {
					continue;
				}
				//	发送消息
				one.second->sendOneFrameText(msgs[1]);
			}
		}
		//	指定发送
		else {
			//	因为要使用conn_pool因此要加锁
			std::lock_guard<std::mutex> guard(listener_mutex);
			//	找iter是否存在
			auto iter = conn_pool->find(msgs[0]);
			//	如果存在则发送信息
			if (iter != conn_pool->end()) {
				iter->second->sendOneFrameText(msgs[1]);
			}
			socket.sendOneFrameText("message send success");
		}
	}
	//	 消息帧接收中 此时就单纯将数据写入缓冲区
	else if (size>v_int64(0)) {
		m_messageBuffer.writeSimple(data, v_buff_size(size));
	}	
}
```

#### WSInstanceListener

> WSInstanceListener.h

```cpp
#ifdef HTTP_SERVER_DEMO
#ifndef _WSINSTANCELISTENER_H_
#define _WSINSTANCELISTENER_H_
#include "oatpp-websocket/ConnectionHandler.hpp"
#include <map>

/**
 * 定义示例WS实例监听器
 */
class WSInstanceListener : public oatpp::websocket::ConnectionHandler::SocketInstanceListener
{
private:
    //	用于日志输出,标志日志的来源
	static constexpr const char* TAG = "Server_WSInstanceListener";
public:
	//	一个原子变量,用来记录当前连接WebSocket的客户端的数量. 原子变量可以保证再多线程环境下操作的安全性,防止竞态条件发生
	static std::atomic<v_int32> SOCKETS;
	// 定义一个连接对象池 -- 来管理活跃的连接
	std::map<std::string, const WebSocket*> conn_pool;
	// 定义一个锁对象 -- 用于保护对连接池的访问
	std::mutex instance_mutex;
public:
	// 当socket实例创建时调用 -- 定义新连接的初始化操作
	void onAfterCreate(const WebSocket& socket, const std::shared_ptr<const ParameterMap>& params) override;
	// 当socket实例销毁前调用 -- 在连接销毁前执行清理动作
	void onBeforeDestroy(const WebSocket& socket) override;
};

#endif // !_WSINSTANCELISTENER_H_
#endif // HTTP_SERVER_DEMO
```

> WSInstanceListener.cpp

```cpp
#include "stdafx.h"

#ifdef HTTP_SERVER_DEMO
#include "WSInstanceListener.h"
#include "WSListener.h"
#include <memory>

//	静态原子计数器 初始化为0
std::atomic<v_int32> WSInstanceListener::SOCKETS(0);
//							socket -- 新建立的连接对象 				params -- 连接建立时传递的参数,一般包含客户端的id
void WSInstanceListener::onAfterCreate(const WebSocket& socket, const std::shared_ptr<const ParameterMap>& params)
{
	// 获取客户端ID
	std::string id = params->at("id")->c_str();
	// 判断客户端对象是否存在
	std::lock_guard<std::mutex> guard(instance_mutex);
	if (conn_pool.find(id) != conn_pool.end()) {
		// 服务器会拒绝新的连接 并关闭socket
		socket.sendClose(9999, u8"reason id has been used");
		OATPP_LOGD(TAG, "New Incoming Connection. Connection has been refuse.");
		return;
	}

	// 添加到连接池中
	conn_pool.insert(std::make_pair(id, &socket));
	OATPP_LOGD(TAG, "client(%s): open connection", id.c_str());

	// 连接数量计数
	SOCKETS++;
	OATPP_LOGD(TAG, "New Incoming Connection. Connection count=%d", SOCKETS.load());

	// 添加消息处理监听器
	socket.setListener(std::make_shared<WSListener>(id, &conn_pool));
}

void WSInstanceListener::onBeforeDestroy(const WebSocket& socket)
{
	auto peer = std::static_pointer_cast<WSListener>(socket.getListener());
	if (peer)
	{
		// 获取客户端ID
		std::string id = peer->getId();

		// 处理客户端移除
		OATPP_LOGD(TAG, "client(%s): close connection", id.c_str());

		// 将连接对象从map中移除
		std::lock_guard<std::mutex> guard(instance_mutex);
		conn_pool.erase(id);
		socket.setListener(nullptr);

		// 连接数量计数
		SOCKETS--;
		OATPP_LOGD(TAG, "Connection closed. Connection count=%d", SOCKETS.load());
	}
}

#endif // HTTP_SERVER_DEMO
```

#### WSController

> WSController.h

```cpp
#pragma once
#ifndef _WS_CONTROLLER_H_
#define _WS_CONTROLLER_H_

#include "ApiHelper.h"
#include "oatpp-websocket/Handshaker.hpp"

#include OATPP_CODEGEN_BEGIN(ApiController)

//	测试WebSocket 访问端点创建
class WSController : public oatpp::web::server::api::ApiController {
	API_ACCESS_DECLARE(WSController);
private:
    //	取出一个名为websocket的组件用于管理WebSocket服务
	OATPP_COMPONENT(std::shared_ptr<oatpp::network::ConnectionHandler>, websocketConnectionHandler, "websocket");
public:
    //	这个端点主要用于处理WebSocket的握手请求				//	请求信息会被该宏解析然后放在request中
	ENDPOINT(API_M_GET, "chat", chat, REQUEST(std::shared_ptr<IncomingRequest>, request)) {
        //	该方法用于执行WebSocket的服务器端握手操作,他接受请求头,和组件,并返回一个响应对象
		auto response = oatpp::websocket::Handshaker::serversideHandshake(request->getHeaders(), websocketConnectionHandler);
        //	创建一个ParameterMap对象 并将请求中的id参数放入其中,这个id参数通常用于识别客户端
		auto parameters = std::make_shared<oatpp::network::ConnectionHandler::ParameterMap>();
		(*parameters)["id"] = request->getQueryParameter("id");
        //	使用该方法将参数附加到响应中,以便在升级连接中使用这些参数
		response->setConnectionUpgradeParameters(parameters);
        //	返回响应对象,完成WebSocket握手
		return response;
	}
};

#include OATPP_CODEGEN_END(ApiController)
#endif // !_WS_CONTROLLER_H_
```

### 封装的开闭原则

**开闭原则(Open/Closed Principle,OCP)**

​		其要求一个软件实体(类,模块,函数等)应该对扩展开放,对修改关闭.

**如何通过封装实现开闭原则**

1. **接口和抽象类**：
   - 通过定义接口或抽象类，将通用行为抽象出来，使具体实现类可以继承或实现这些接口。
   - 当需要扩展功能时，可以新增实现类，而不需要修改原有的代码。
2. **依赖倒置**：
   - 高层模块不应该依赖于低层模块，二者都应该依赖于抽象。通过依赖接口或抽象类，业务逻辑与具体实现解耦。
   - 当需要修改某个功能时，可以通过提供新的实现类，而不需要改变高层模块。
3. **策略模式**：
   - 通过定义一系列算法，将它们封装到独立的类中，并使它们可以互相替换。这样，当需要扩展新的算法时，只需新增一个策略类，而不需要修改现有代码。
4. **模板方法模式**：
   - 在一个方法中定义算法的骨架，而将一些步骤延迟到子类中实现。通过继承和重写，可以在不改变算法结构的情况下扩展新的功能。

**示例**

假设你在封装一个支付系统，初始版本只有信用卡支付功能。你可以通过以下方式来遵循开闭原则：

```cpp
// 抽象支付接口
class PaymentProcessor {
public:
    virtual void processPayment(double amount) = 0;
    virtual ~PaymentProcessor() = default;
};

// 信用卡支付实现
class CreditCardProcessor : public PaymentProcessor {
public:
    void processPayment(double amount) override {
        // 信用卡支付逻辑
        std::cout << "Processing credit card payment: " << amount << std::endl;
    }
};

// 支付上下文，依赖于抽象类
class PaymentContext {
private:
    PaymentProcessor* processor;
public:
    PaymentContext(PaymentProcessor* p) : processor(p) {}
    void pay(double amount) {
        processor->processPayment(amount);
    }
};

// 现在你要扩展添加新的支付方式，比如 PayPal
class PayPalProcessor : public PaymentProcessor {
public:
    void processPayment(double amount) override {
        // PayPal 支付逻辑
        std::cout << "Processing PayPal payment: " << amount << std::endl;
    }
};
```

在上面的例子中，当需要扩展新的支付方式（如 PayPal）时，只需要添加一个新的 `PayPalProcessor` 类，而无需修改原有的 `PaymentProcessor` 接口或 `PaymentContext` 类的代码，这就实现了对扩展开放、对修改关闭的设计

## 消息中间件

![image-20240822130407821](C:\Users\Luk1\AppData\Roaming\Typora\typora-user-images\image-20240822130407821.png)

但在本次项目中,采用了alibaba的`RocketMQ`.(实际上这个中间件跟Java生态更适配)

### TestRocket

> TestRocket.h

```cpp
ifndef _TESTROCKET_H_
#define _TESTROCKET_H_
#include "RocketClient.h" //引入客户端操作
#include <memory>		//引入智能指针

/**
 * 测试RocketMQ
 */
class TestRocket : public RocketClient::RConsumerListener	//	消费者监听器,它可以接受和处理ROcketMQ的消息
{
private:
	std::shared_ptr<RocketClient> client;					//	负责管理client的生命周期
	std::shared_ptr<RocketClient::RSendCallback> cb;		//	用于处理消息发送的回调函数的智能指针
public:
	TestRocket();
	~TestRocket();
	void testRocket();
	void receiveMessage(std::string payload) override;		//	负责接收和处理消息.payload是接收到的消息内容
};
#endif // _TESTROCKET_H_
```

> TestRocket.cpp

````cpp
#include "stdafx.h"
#include "TestRocket.h"
#include "domain/dto/sample/SampleDTO.h"
#include <iostream>


//	构造函数 先置空处理
TestRocket::TestRocket() {
	this->client = nullptr;
	this->cb = nullptr;
}
//	析构函数
TestRocket::~TestRocket() {
	// 检查客户端是否存在,如果存在则取消订阅 确保客户端资源正确释放,因为是共享指针因此不用管
    if (client) {
		client->unsubscribe();
	}
}

void TestRocket::testRocket() {
	//	创建客户端
	client = make_shared<RocketClient>("192.168.136.132:9876");
	//	创建发送回调函数   用于在发送信息后处理发送状态 
	cb = make_shared<RocketClient::RSendCallback>([](SendStatus status)
		{
			std::cout << "RSendCallback send status: " << status << endl;
		});
	//	测试开始订阅
    //	订阅hello主题
	client->subscribe("hello");
    //	绑定监听器是自己
	client->addListener(this);
	//	定义消费对象
	auto dto = SampleDTO::createShared();
	dto->name = "cat";
	dto->sex = "man";
	dto->age = 10;
	//	发送消息
	dto->id = 1;
    //	异步发送 调用cb处理结果
	RC_PUBLISH_OBJ_MSG_ASYNC(client, "hello", dto, cb.get());
	dto->id = 2;
    //	异步发送 不处理结果
	RC_PUBLISH_OBJ_MSG_ASYNC(client, "hello", dto, nullptr);
	dto->id = 3;
    //	同步发送 并将结果存储在res1中
	RC_PUBLISH_OBJ_MSG_SYNC(res1, client, "hello", dto);
	std::cout << "sync send result: " << res1 << endl;
}
void TestRocket::receiveMessage(std::string payload) {
    //	用于将payload转化成dto (反序列化) json -> dto
	RC_RECEIVER_MSG_CONVERT(dto, SampleDTO, payload);
    //	拼接输出到控制台
	std::cout << "receivedMessage: " << dto->id.getValue(-1)
		<< "-" << dto->name.getValue("")
		<< "-" << dto->sex.getValue("")
		<< "-" << dto->age.getValue(0)
		<< endl;
}
````



## 权限认证

采用了RBAC(Role-Based Access Control)的模式

### API_ACCESS_DECLARE

```CPP
 /**
 * 控制器类访问定义，用于绑定授权处理器和类创建入口函数
 * @param __CLASS__: controller类名称
 */
#define API_ACCESS_DECLARE(__CLASS__) \
public: \
//	每一个Controller类的构造函数 在初始化列表用objectMapper组件初始化了ApiController 同时在函数实现中 设置了默认的权限处理器
__CLASS__(OATPP_COMPONENT(std::shared_ptr<ObjectMapper>, objectMapper)) : //
oatpp::web::server::api::ApiController(objectMapper) { \
    //	这意味着每当这个控制器处理请求时，都会先经过这个授权处理器，确保请求是经过授权的
	setDefaultAuthorizationHandler(std::make_shared<CustomerAuthorizeHandler>()); \
} \
//	创建了一个静态的工厂方法来创建控制器类的实例。同样接收一个objectMapper组件来初始化该类
static std::shared_ptr<__CLASS__> createShared(OATPP_COMPONENT(std::shared_ptr<ObjectMapper>, objectMapper)) { \
	return std::make_shared<__CLASS__>(objectMapper); \
}
```

### TestToken

> TestToken.h

```cpp
#pragma once
#ifndef _TEST_TOKEN_H_
#define _TEST_TOKEN_H_

//	测试JWT Token
class TestToken
{
public:
	static void generateToken();
};

#endif // !_TEST_TOKEN_H_

```

> TestToken.cpp

```cpp
#include "stdafx.h"
#include "TestToken.h"
#include "JWTUtil.h"
#include <iostream>

void TestToken::generateToken()
{
    //	实例化对象 -- 一个存储 JWT 负载数据的DTO
	PayloadDTO p;
    //	向 authorities 容器中添加权限
	p.getAuthorities().push_back("SUPER_ADMIN");
    //	设置用户名
	p.setUsername(u8"roumiou");
	//	设置用户编号
    p.setId("1");
    //	设置凭证有效时常为 3600(1h) * 30 = 30h
	p.setExp(3600 * 30);
    //	打印 JWT
	std::cout << JWTUtil::generateTokenByRsa(p, RSA_PRIV_KEY->c_str()) << std::endl;
}
```

#### JWT是什么?

**JWT(Json Web Token)** 是一种用于安全的传输信息的开放标准(RFC 7519).他被广泛的用于身份验证和信息交换.JWT通常用于以下几种场景

1. **身份验证**

   JWT可以在用户登录后生成,并在用户后续请求中传递,以验证用户身份,服务器可以使用JWT来确认用户的身份和权限

2. **信息交换**

   JWT可以用于在各方之间安全的传输信息,因为JWT可以签名以验证信息的完整性

#### RSA 私钥和公钥及其在 JWT 中的作用

**RSA（Rivest-Shamir-Adleman）** 是一种常用的非对称加密算法，它使用一对密钥：私钥和公钥。

1. **RSA 私钥**：用于签名 JWT。只有持有私钥的一方能够创建有效的签名。
   - 在 JWT 签名过程中，JWT 的头部和负载会被编码成字符串，然后使用 RSA 私钥对这些数据进行加密，生成签名部分。
   - 这个签名可以保证 JWT 的内容在传输过程中未被篡改，因为只有对应的私钥可以生成有效的签名。
2. **RSA 公钥**：用于验证 JWT 的签名。持有公钥的一方可以使用它来检查 JWT 的签名是否有效，从而确认 JWT 的内容是否可信。
   - 在验证过程中，接收方使用 RSA 公钥对 JWT 的签名进行解密，得到签名的原始数据，然后与 JWT 的头部和负载重新计算的签名进行比较。如果两者匹配，则证明 JWT 的内容没有被篡改。

### PayLoadDTO

> PayloadDTO.h

```cpp
#ifndef _PAYLOADDTO_H_
#define _PAYLOADDTO_H_
#include "jwt/jwt.hpp"

/**
 * 负载信息获取状态编码
 */
enum class PayloadCode
{
	// 信息验证处理成功
	SUCCESS,
	// Token已过期
	TOKEN_EXPIRED_ERROR,
	// 签名格式错误
	SIGNATUREFORMAT_ERROR,
	// 解密错误
	DECODE_ERROR,
	// 验证错误
	VERIFICATION_ERROR,
	// 其他错误
	OTHER_ERROR
};

/**
 * 负载信息实体类
 */
class PayloadDTO
{
public:
	// 获取状态码对应的枚举值名称
	static std::string getCodeName(PayloadCode code) 
	{
		switch (code)
		{
		case PayloadCode::SUCCESS:
			return "SUCCESS";
		case PayloadCode::TOKEN_EXPIRED_ERROR:
			return "TOKEN_EXPIRED_ERROR";
		case PayloadCode::SIGNATUREFORMAT_ERROR:
			return "SIGNATUREFORMAT_ERROR";
		case PayloadCode::DECODE_ERROR:
			return "DECODE_ERROR";
		case PayloadCode::VERIFICATION_ERROR:
			return "VERIFICATION_ERROR";
		case PayloadCode::OTHER_ERROR:
			return "OTHER_ERROR";
		default:
			return "NONE";
		}
	}
private:
	// 主体数据
	std::string sub;
	// 凭证有效时长（秒）
	int64_t exp;
	// 用户编号
	std::string id;
	// 用户名
	std::string username;
	// 用户拥有的权限
	std::list<std::string> authorities;
	// 数据状态系信息
	PayloadCode code;
public:
    //	构造函数 初始化为相关值
	PayloadDTO()
	{
		this->username = "";
		this->exp = 0;
		this->sub = "";
		this->setCode(PayloadCode::SUCCESS);
	}
    //	有参构造
	PayloadDTO(std::string _sub, int64_t _exp, std::string _username, std::list<std::string> _authorities) :
		sub(_sub), exp(_exp), username(_username), authorities(_authorities)
	{
		this->setCode(PayloadCode::SUCCESS);
	}
	
	// getter/setter
	std::string getSub() const { return sub; }
	void setSub(std::string val) { sub = val; }
	int64_t getExp() const { return exp; }
	void setExp(int64_t val) { exp = val; }
	std::string getUsername() const { return username; }
	void setUsername(std::string val) { username = val; }
	std::list<std::string>& getAuthorities() { return authorities; }
	void setAuthorities(std::list<std::string> val) { authorities = val; }
	PayloadCode getCode() const { return code; }
	void setCode(PayloadCode val) { code = val; }
	std::string getId() const { return id; }
	void setId(std::string val) { id = val; }

	// 添加权限
	void putAuthority(std::string authstr) { authorities.push_back(authstr); }
	
	// 将Payload的属性转换到jwt_object中
	// 注意：新增属性字段后需要维护此方法
	template<class T>
	void propToJwt(T* obj) const
	{
		// 转换权限列表
		obj->add_claim("authorities", authorities);
		// 转换用户名
		obj->add_claim("user_name", username);
		// 转换id
		obj->add_claim("id", id);
		// TIP：新增字段在后面补充即可
	}

	// 将jwt_object的属性转换到Payload中
	// 注意：新增属性字段后需要维护此方法 -- 这里的porp是指 properties(属性)
	void propToPayload(jwt::jwt_object* obj) 
	{
		// 获取负载信息
		auto payload = obj->payload();
		auto _payload = payload.create_json_obj();

		// 转换权限列表
		if (_payload.contains("authorities"))
			setAuthorities(payload.get_claim_value<std::list<std::string>>("authorities"));
		// 转换用户名
		setUsername(payload.get_claim_value<std::string>("user_name"));
		// 转换数字类型id
		if (_payload["id"].is_number()) 
			setId(std::to_string(_payload["id"].get<int64_t>()));
		// 转换字符串类型id
		else
			setId(_payload["id"].get<std::string>());
		// TIP：新增字段在后面补充即可
	}
};

#endif // !_PAYLOADDTO_H_
```

### SystemInterceptor

#### 系统拦截器

这个是主要用于拦截请求和响应的组件.

- 是指在请求到达Controller之前,或者响应返回给客户端之前执行的特定的逻辑的组件.
  - **权限认证和授权**：在请求到达控制器之前，拦截器可以检查当前请求是否包含有效的 JWT Token（或其他形式的认证信息）。如果没有，拦截器可以直接阻止请求的继续执行，并返回未授权的响应。
  - **请求日志记录**：记录所有进入系统的请求信息，如请求的路径、参数、用户信息等，以便日后追踪和分析。
  - **全局异常处理**：拦截器可以在响应返回给客户端之前，捕获异常并处理，保证系统在异常情况下仍能返回合适的响应。
  - **修改请求/响应**：拦截器可以在请求到达控制器之前或响应返回给客户端之前，修改请求或响应的数据。

##### 网关和拦截器对于权限认证的区别

**网关的职责**:

- 认证：验证用户的身份，例如解析和验证 JWT Token。
- 授权：检查用户是否有权限访问特定的服务或 API。
- 路由：将请求转发到正确的微服务或应用程序。
- 负载均衡：分配请求到不同的服务实例以实现高可用性。
- 限流和监控：防止恶意请求，并监控流量。

**拦截器的职责**:

- 进一步的权限控制：在服务内部根据具体的业务逻辑进一步检查用户的权限，例如用户是否有权限执行特定操作。
- 业务相关的请求处理：如请求参数校验、日志记录、异常处理等。

**网关的权限认证**适用于**全局统一**的权限控制，尤其是在微服务架构中，网关作为统一入口，能够有效减少各个服务重复实现认证逻辑的开销。

**拦截器的权限认证**适用于**服务内部**的细粒度权限控制。例如，一个用户即使通过了网关的认证，当他访问特定的服务或 API 时，拦截器可以进一步检查他是否有访问该特定资源的权限。

#### 源码

> SystemInterceptor.h

```cpp
#ifndef _SYSTEMINTERCEPTOR_H_
#define _SYSTEMINTERCEPTOR_H_
#include "oatpp/web/server/interceptor/RequestInterceptor.hpp"
#include "oatpp/web/server/interceptor/ResponseInterceptor.hpp"

/**
 * 跨域请求拦截器
 */
class CrosRequestInterceptor : public oatpp::web::server::interceptor::RequestInterceptor
{
public:
	// 拦截器执行逻辑
	std::shared_ptr<OutgoingResponse> intercept(const std::shared_ptr<IncomingRequest>& request) override;
/*
	这是拦截器的核心方法用于拦截和处理传入的http请求
	在这个方法中,你可以对请求进行检查和修改,或者阻止请求继续传递
	在跨域请求的上下文中,这个拦截器通常用于处理 CORS 相关的请求头,确保客户端能够合法的跨域访问资源
*/
};

/**
 * 跨域响应拦截器
 */
class CrosResponseInterceptor : public oatpp::web::server::interceptor::ResponseInterceptor {
public:
	// 拦截器执行逻辑
	std::shared_ptr<OutgoingResponse> intercept(const std::shared_ptr<IncomingRequest>& request, const std::shared_ptr<OutgoingResponse>& response) override;
/*
	这是响应拦截器的核心方法,用于拦截和处理传出的http响应
	该方法允许在相应发送给客户端之前,对其进行检查和修改.
	对于跨域请求,通常在这里添加CORS响应头,如`Access-Control-Allow-Origin`等,以便语序跨域资源共享
*/
}

/**
 * 校验凭证请求拦截器
 */
class CheckRequestInterceptor : public oatpp::web::server::interceptor::RequestInterceptor
{
private:
	// DTO序列化对象 一个映射器 因为在检验请求时拦截器可能需要在请求中解析数据,因此要用到
	std::shared_ptr<oatpp::data::mapping::ObjectMapper> m_objectMapper;
public:
	// 构造的时候传入数据序列化对象
	explicit CheckRequestInterceptor(const std::shared_ptr<oatpp::data::mapping::ObjectMapper>& objectMapper);
	// 拦截器执行逻辑
	std::shared_ptr<OutgoingResponse> intercept(const std::shared_ptr<IncomingRequest>& request) override;
/*
	这是请求拦截器的核心方法,用于拦截和处理传入的http请求
	该方法可以用来校验请求中是否包含有效的凭证或认证信息
	如果校验失败,拦截器可以直接返回一个错误响应,组织请求继续处理
*/
};


#endif // !_SYSTEMINTERCEPTOR_H_
```

>SystemInterceptor.cpp

```cpp
#ifndef CHECK_TOKEN
// 开启凭证检查，解开下一行注释即可
#define CHECK_TOKEN
#endif

// 定义一个临时凭证
std::unique_ptr<std::string> TMP_TOKEN = nullptr;

// 测试负载数据初始化
#define TEST_PAYLOAD_INIT \
PayloadDTO payload; \
payload.setExp(3600 * 30); \
payload.setId("1"); \
payload.setUsername(u8"admin"); \
payload.putAuthority("ADMIN"); \
payload.putAuthority("TEST"); \
TMP_TOKEN = std::make_unique<std::string>("Bearer " + JWTUtil::generateTokenByRsa(payload, RSA_PRIV_KEY->c_str()));

// 跨域属性设置 -- 添加跨域相关的 HTTP 头
#define CROS_FIELD_SETTING(__RES__) \
__RES__->putHeaderIfNotExists("Access-Control-Allow-Origin", "*"); \
__RES__->putHeaderIfNotExists("Access-Control-Allow-Methods", "*"); \
__RES__->putHeaderIfNotExists("Access-Control-Expose-Headers", "*"); \
__RES__->putHeaderIfNotExists("Access-Control-Allow-Credentials", "true"); \
__RES__->putHeaderIfNotExists("Access-Control-Allow-Headers", "Content-Type,Access-Token");
//	Access-Control-Allow-Origin , * -> 允许所有源访问
//	Access-Control-Allow-Method , * -> 允许所有方法

std::shared_ptr<oatpp::web::server::interceptor::RequestInterceptor::OutgoingResponse> CrosRequestInterceptor::intercept(const std::shared_ptr<IncomingRequest>& request)
{
#ifndef CLOSE_CROS_SUPPORT
	//	从请求中提取方法
	auto method = request->getStartingLine().method;
	//	如果是 OPTIONS那就返回resp
	if (method == "OPTIONS")
	{
		//	创建响应实体同时添加跨域相关的头
		auto res = OutgoingResponse::createShared(Status::CODE_200, nullptr);
		CROS_FIELD_SETTING(res)
		return res;
	}
#endif
	//	如果关闭了跨域支持那就返回空指针
	return nullptr;
}

std::shared_ptr<oatpp::web::server::interceptor::ResponseInterceptor::OutgoingResponse> CrosResponseInterceptor::intercept(const std::shared_ptr<IncomingRequest>& request, const std::shared_ptr<OutgoingResponse>& response)
{
#ifndef CLOSE_CROS_SUPPORT
	CROS_FIELD_SETTING(response)
#endif
	return response;
}

std::shared_ptr<Response> createErrorRespone(std::string message, std::shared_ptr<oatpp::data::mapping::ObjectMapper> mapper) {
	auto error = NoDataJsonVO::createShared();
	error->init(RS_UNAUTHORIZED);
	error->message = message;
	auto response = ResponseFactory::createResponse(Status::CODE_200, error, mapper);
	return response;
}

CheckRequestInterceptor::CheckRequestInterceptor(const std::shared_ptr<oatpp::data::mapping::ObjectMapper>& objectMapper)
{
	m_objectMapper = objectMapper;
#ifndef CHECK_TOKEN
	// 初始化一个凭证
	TEST_PAYLOAD_INIT
#endif
}

std::shared_ptr<oatpp::web::server::interceptor::RequestInterceptor::OutgoingResponse> CheckRequestInterceptor::intercept(const std::shared_ptr<IncomingRequest>& request)
{
	auto path = request->getStartingLine().path.toString().getValue("");
	auto method = request->getStartingLine().method.toString().getValue("");
	auto protocol = request->getStartingLine().protocol.toString().getValue("");
	//	记录日志
	OATPP_LOGD("Interceptor", "%s:%s->%s", protocol.c_str(), method.c_str(), path.c_str());
	// Swagger文档与关闭服务器请求不拦截 (相当于请求的白名单)
	if (path.find("/chat?") == 0 ||
		path.find("/swagger/") == 0 || 
		path.find("/api-docs/") == 0 || 
		path.find("/system-kill/") == 0)
	{
		return nullptr;
	}
#ifdef CHECK_TOKEN
	// 获取请求凭证
	oatpp::String token = request->getHeader("Authorization");
	if (!token || token->empty()) {
		//	如果凭证为空或无效，则返回一个包含错误信息的响应
		return createErrorRespone("empty token", m_objectMapper);
	}
#else
	request->putHeaderIfNotExists("Authorization", TMP_TOKEN->c_str());
#endif
	return nullptr;
}
```

#### 跨域是什么?

跨域（Cross-Origin）是指当浏览器中的一个页面发起的请求，其目标地址的域名、协议或端口号与当前页面所在的地址不同。这种跨域请求由于浏览器的同源策略（Same-Origin Policy）会受到限制，以确保安全。

##### **什么是同源策略？**

同源策略是一种浏览器的安全机制，用于防止恶意网站通过代码操作用户在其他网站的内容。根据同源策略，只有当两个页面具有相同的协议、域名和端口号时，它们才被认为是同源的。否则，它们就是跨域的。

- **同源**：`http://example.com/page` 与 `http://example.com/data` 是同源的。
- **跨域**：`http://example.com/page` 与 `https://example.com/data` 或 `http://api.example.com/data` 是跨域的。

##### **跨域的常见场景**

1. 不同域名：
   - 例如：`http://example.com` 和 `http://another.com`。
2. 不同子域名：
   - 例如：`http://app.example.com` 和 `http://api.example.com`。
3. 不同协议：
   - 例如：`http://example.com` 和 `https://example.com`。
4. 不同端口号：
   - 例如：`http://example.com:8080` 和 `http://example.com:8081`。

##### **为什么需要跨域？**

在实际应用中，跨域请求是非常常见的。例如：

- 前端页面在 `example.com` 上，可能需要从 `api.example.com` 获取数据。
- 前端页面使用了CDN资源，这些资源可能来自不同的域名。

### AuthorizationHandler

> AuthorizationHandler.h

```cpp
#ifndef _CUSTOMERAUTHORIZEHANDLER_H_
#define _CUSTOMERAUTHORIZEHANDLER_H_
#include "oatpp/web/server/handler/AuthorizationHandler.hpp"
#include "JWTUtil.h"

/**
 * 自定义授权实体数据实体
 */
class CustomerAuthorizeObject : public oatpp::web::server::handler::AuthorizationObject
{
private:
	// 负载数据记录实体
	PayloadDTO payload;
public:
	// 构造初初始化
	CustomerAuthorizeObject(PayloadDTO payload);
	// 获取负载数据对象
	const PayloadDTO& getPayload();
};

/**
 * 自定义授权处理器
 */
class CustomerAuthorizeHandler : public oatpp::web::server::handler::BearerAuthorizationHandler
{
public:
	// 构造初始化公钥读取
	CustomerAuthorizeHandler();
	// 授权逻辑
	std::shared_ptr<AuthorizationObject> authorize(const oatpp::String& token) override;
};

#endif // _CUSTOMERAUTHORIZEHANDLER_H_
```

>AuthorizationHandler.cpp

```cpp
#include "pch.h"
#include <sstream>
#include <string>
#include <iostream>
#include <fstream>
#include "../include/CustomerAuthorizeHandler.h"

// std::unique_ptr<std::string> RSA_PUB_KEY = std::make_unique<std::string>(R"(
// -----BEGIN PUBLIC KEY-----
// MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA2CUog6kdKUOlOtdOHFcs
// ts0KHt5eg8UPF6Yj/jte7jgxOWsYB571rdMzTDIYo1UIaYVOJcd3oio9QlebUZD7
// O4GL8oJmj9rNCVk60xfx3vhYISzdHbwQhUUgx+YDmDr5UJV/D/uhCdFKziTUBMjD
// otSQXvCsbWIMGGEFbPXKe9VRmgqtjdNfWvjMa7spQwiy0gj7GeOUiIttkVZna6qF
// FZRSRAxp3NJ9ELbcW7Kd9u5IFzrvxXNiYPOtIiw+zqJTYsSXUJTI7YQAXy9zqGtT
// 7QUFUjxUf+7b1DELpGZPmwGd5Jzj+zfTNsS3DRNuPQJPkPbpUo1qCsU55sXgcNrf
// zwIDAQAB
// -----END PUBLIC KEY-----)");

// RSA公钥
std::unique_ptr<std::string> RSA_PUB_KEY = nullptr;

CustomerAuthorizeObject::CustomerAuthorizeObject(PayloadDTO payload)
{
	this->payload = payload;
}

const PayloadDTO& CustomerAuthorizeObject::getPayload()
{
	return this->payload;
}

CustomerAuthorizeHandler::CustomerAuthorizeHandler()
{
	//读取公钥
	if (!RSA_PUB_KEY)
	{
		std::string pubKey = "";
		std::ifstream ifs("public.pem");
		if (ifs.is_open())
		{
			std::string tmp;
			while (std::getline(ifs, tmp))
			{
				pubKey += tmp + "\n";
			}
			ifs.close();
		}
		RSA_PUB_KEY = std::make_unique<std::string>(pubKey);
	}
}

std::shared_ptr<oatpp::web::server::handler::AuthorizationHandler::AuthorizationObject> CustomerAuthorizeHandler::authorize(const oatpp::String& token)
{
	// 解析凭证
	PayloadDTO payload = JWTUtil::verifyTokenByRsa(token, RSA_PUB_KEY->c_str());
    //	错误处理
	if (payload.getCode() != PayloadCode::SUCCESS) {
		std::stringstream ss;
		ss << "Token: check fail code <" << PayloadDTO::getCodeName(payload.getCode()) << ">.";
		throw std::logic_error(ss.str());
	}
	// 将数据存放到授权对象中
	return std::make_shared<CustomerAuthorizeObject>(payload);
}

```

### JWTUtils

> JWTUtils.h

```cpp
#ifndef _JWT_UTIL_
#define _JWT_UTIL_
#include "jwt/jwt.hpp"
#include <openssl/md5.h>
#include <list>
#include <memory>
#include "domain/dto/PayloadDTO.h"
using namespace jwt;

/**
 * JWT工具类
 */
class JWTUtil
{
private:
	//对字符串进行MD5处理 -- 对字符串进行md5哈希处理.这个方法在 HMAC 相关的处理的时候可能会用到
	static std::string md5(const std::string& src);
public:
	//************************************
	// Method:    generateTokenByHmac
	// FullName:  JWTUtil::generateTokenByHmac
	// Access:    public static 
	// Returns:   std::string 返回Token字符串
	// Qualifier: 使用HMAC算法构建Token
	// Parameter: const PayloadDTO& payloadDto 负载信息对象
	// Parameter: const std::string& secretStr 秘钥
	//************************************
	static std::string generateTokenByHmac(const PayloadDTO& payloadDto, const std::string& secretStr);
    
    
	//************************************
	// Method:    verifyTokenByHmac
	// FullName:  JWTUtil::verifyTokenByHmac
	// Access:    public static 
	// Returns:   PayloadDTO 负载信息对象
	// Qualifier: 验证HMAC签名的 Token
	// Parameter: const std::string& token Token字符串
	// Parameter: const std::string& secretStr 秘钥
	//************************************
	static PayloadDTO verifyTokenByHmac(const std::string& token, const std::string& secretStr);

	//************************************
	// Method:    generateTokenByRsa
	// FullName:  JWTUtil::generateTokenByRsa
	// Access:    public static 
	// Returns:   std::string
	// Qualifier: 使用RSA Pem生成Token，密钥对在线生成工具：http://www.metools.info/code/c80.html
	// Parameter: const PayloadDTO& payloadDto 负载信息
	// Parameter: const std::string& rsaPriKey RSA私钥
	//************************************
	static std::string generateTokenByRsa(const PayloadDTO& payloadDto, const std::string& rsaPriKey);

	//************************************
	// Method:    verifyTokenByRsa
	// FullName:  JWTUtil::verifyTokenByRsa
	// Access:    public static 
	// Returns:   PayloadDTO
	// Qualifier: 验证RSA Pem Token
	// Parameter: const std::string& token Token字符串
	// Parameter: const std::string& rsaPubKey RSA公钥
	//************************************
	static PayloadDTO verifyTokenByRsa(const std::string& token, const std::string& rsaPubKey);
};

// 测试RSA私钥
extern std::unique_ptr<std::string> RSA_PRIV_KEY;
#endif // !_JWT_UTIL_

```

> JWTUtils.cpp

```cpp
#include "pch.h"
#include <iostream>
#include "JWTUtil.h"

// 定义一个测试RSA私钥
std::unique_ptr<std::string> RSA_PRIV_KEY = std::make_unique<std::string>(R"(
-----BEGIN PRIVATE KEY-----
MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQDYJSiDqR0pQ6U6
104cVyy2zQoe3l6DxQ8XpiP+O17uODE5axgHnvWt0zNMMhijVQhphU4lx3eiKj1C
V5tRkPs7gYvygmaP2s0JWTrTF/He+FghLN0dvBCFRSDH5gOYOvlQlX8P+6EJ0UrO
JNQEyMOi1JBe8KxtYgwYYQVs9cp71VGaCq2N019a+MxruylDCLLSCPsZ45SIi22R
VmdrqoUVlFJEDGnc0n0Qttxbsp327kgXOu/Fc2Jg860iLD7OolNixJdQlMjthABf
L3Ooa1PtBQVSPFR/7tvUMQukZk+bAZ3knOP7N9M2xLcNE249Ak+Q9ulSjWoKxTnm
xeBw2t/PAgMBAAECggEADHXH6h8boT9XDRdQV23nE/qp9LGY/Tuk7RYUyRkfFdiD
be3wiq/tNcIRGPliVjgWrg6TPLZM/To2IdbvCzqyYPHM4YQG6ZARddKBA55DwTjL
y83MSWSIB0a+5wcpeeMccDrOAlvdIrW//DY/Sq9QJ9jdIbv6FKwsSlN9fpSEwbKl
TDqwZJCyc5KBKq7r6NixO/ksATi1uaQUfJT5b4sakGKUN5I7MwAjST4em7Ze8VVc
HGt1ClaTgLxKfPMurd0Ec+8o/3ex/PkU7Wx8AHqAj/IQsLdNB2arHePpcQVzHjsb
u4+zJSrtxOzrZlC/qfPObh8+o/i72K556ZfcEFjb8QKBgQDt2qD5sKn592+xtGXX
rzv/8G1CdE6Zy4WBUl33gov2rbGvmkrAeDGWV7dgTW0fPI9oXhV4Ioc7q61cDp8C
U9FDjDNpEEhUextq4VFjJWQ2tUvigyTkMFT7dEg1j35jbMGmvNh9jWQzdeM3Rheb
Q8VVGbZ5i2z4iGpfrDfStUeiiwKBgQDooow36Y5KZtvbnkF+C0nqQ7LC63ZsSBTS
UQgFWw5sBJssv9DsZIm1Ke14aHZftrDm67mg+/xsrw3+DZxwlaui8zA4PLpmTrGj
AnJ/2F9En8LZtb/ove+gXuQjZrNUsHh6+OpMWaEC1Flp3+jaPoaKZPp0ta/WYHPi
OEQ3uvh0TQKBgH0FvjeAtNe/R+aQfDey1EbjiYq0t9v/Ll2bfejrpcYz5oH3B/PD
Oc1crfbgu8r/eiHR0lcjTxH+W1FYHhyLEiP/Pcar2FkPnInBhZYnwVVAVnLpnCqV
fRXvOUVt93EraV7LRMA54cFq5dPX8/CY3tCsg03AC7dXfRJs46rNvqmhAoGACyR1
+Nub8B5bG3rKAkKCKNFTR5jFlEwjiytMag1BdJUH5a3OUPRD0ESQ1jqSqOT0NitG
Odq37XC5B9kZDB9vGB/zyE3IU8wjH/6nA06WyY+pYoodBgXK63CAFt39auoE60bu
2fdVCfCn07Vgzss94HUTtfFZ2bfG9SfixJSU/+UCgYEAyW1Si7qQRiNUSJWU8Jae
yFWOL1mvZRpXPUlg70H4wARoJjK6XgNKcE6GWbOedNtyiVJ7b07bmf9YJX2NWOzE
913vLOeLSlJeJAoQHEoYCM0nnOEcfUMiuOx59R4zk4RzSC64uK9PeguGSS6RaQwQ
8aj6l5u1SVtUNRb+ZjPCU8c=
-----END PRIVATE KEY-----)");

#define JU_VERIFY_CATCH(__p__) \
catch (const jwt::TokenExpiredError& e) { \
	std::cerr << "TokenExpiredError:" << e.what() << std::endl; \
	__p__.setCode(PayloadCode::TOKEN_EXPIRED_ERROR); \
} \
catch (const jwt::SignatureFormatError& e) { \
	std::cerr << "SignatureFormatError:" << e.what() << std::endl; \
	__p__.setCode(PayloadCode::SIGNATUREFORMAT_ERROR); \
} \
catch (const jwt::DecodeError& e) { \
	std::cerr << "DecodeError:" << e.what() << std::endl; \
	__p__.setCode(PayloadCode::DECODE_ERROR); \
} \
catch (const jwt::VerificationError& e) { \
	std::cerr << "VerificationError:" << e.what() << std::endl; \
	__p__.setCode(PayloadCode::VERIFICATION_ERROR); \
} \
catch (const std::exception& e) { \
	std::cerr << "OtherError:" << e.what() << std::endl; \
	__p__.setCode(PayloadCode::OTHER_ERROR); \
}

std::string JWTUtil::md5(const std::string& src)
{
	MD5_CTX ctx;
	std::string md5_string;
	unsigned char md[16] = { 0 };
	char tmp[33] = { 0 };
	MD5_Init(&ctx);
	MD5_Update(&ctx, src.c_str(), src.size());
	MD5_Final(md, &ctx);
	for (int i = 0; i < 16; ++i)
	{
		memset(tmp, 0x00, sizeof(tmp));
		snprintf(tmp, sizeof(tmp), "%02X", md[i]);
		md5_string += tmp;
	}
	return md5_string;
}

std::string JWTUtil::generateTokenByHmac(const PayloadDTO& payloadDto, const std::string& secretStr)
{
	//1 创建JWT头，设置签名算法和类型
	jwt_header hdr = jwt_header{ jwt::algorithm::HS256 };
	//2 将负载信息封装到Payload中
	jwt::jwt_payload jp;
	//2.1 呼叫属性转换
	payloadDto.propToJwt(&jp);
	//2.2 失效时间在内部处理
	jp.add_claim("exp", std::chrono::system_clock::now() + std::chrono::seconds{ payloadDto.getExp() });
	//3 创建HMAC签名器
	jwt::jwt_signature sgn{ md5(secretStr) };
	std::error_code ec{};
	//4 生成token
	auto res = sgn.encode(hdr, jp, ec);
	return res;
}

PayloadDTO JWTUtil::verifyTokenByHmac(const std::string& token, const std::string& secretStr)
{
	PayloadDTO p;
	using namespace jwt::params;
	try {
		jwt_object dec_obj = jwt::decode(token, algorithms({ "HS256" }), secret(string_view(md5(secretStr))), verify(true));
		// 呼叫属性转换
		p.propToPayload(&dec_obj);
		// 失效时间在内部处理
		p.setExp(dec_obj.payload().get_claim_value<int64_t>("exp"));
	}
	JU_VERIFY_CATCH(p);
	return p;
}

std::string JWTUtil::generateTokenByRsa(const PayloadDTO& payloadDto, const std::string& rsaPriKey)
{
	jwt::jwt_object obj;
	obj.secret(rsaPriKey);
	obj.header().algo(jwt::algorithm::RS256);
	// 呼叫属性转换
	payloadDto.propToJwt(&obj);
	// 失效时间在内部处理
	obj.add_claim("exp", std::chrono::system_clock::now() + std::chrono::seconds{ payloadDto.getExp() });
	return obj.signature();
}

PayloadDTO JWTUtil::verifyTokenByRsa(const std::string& token, const std::string& rsaPubKey)
{
	PayloadDTO p;
	using namespace jwt::params;
	try {
		jwt_object dec_obj = jwt::decode(token, algorithms({ "RS256" }), secret(rsaPubKey), verify(true));
		// 呼叫属性转换
		p.propToPayload(&dec_obj);
		// 失效时间在内部处理
		p.setExp(dec_obj.payload().get_claim_value<int64_t>("exp"));
	}
	JU_VERIFY_CATCH(p);
	return p;
}
```

## 分层领域规约

### 领域对象描述

- `DO`(Data Object): 此对象与数据库表结构一一对应,通过`DAO`层向上传输数据源对象
- `DTO`(Data Transfer Object): 数据传输对象,Service 或 Manager 向外传输的对象
- `BO`(Business Object): 业务对象,可以由Service 层输出的封装业务逻辑对象
- `Query`: 数据查询对象,各层接受上层的查询请求.注意超过2个参数的查询封装,禁止使用Map类来进行传输
- `VO`(View Object): 显示层对象,通常是 Web 向模板渲染引擎层传输的对象

各层之间的关系如下图所示,包含了领域模型的传递过程

![分层领域规约](F:\project\zero-one-hrsys-1.0.0\hr-cpp\imgs\分层领域规约.png)
