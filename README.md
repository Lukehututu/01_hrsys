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

注意连接excel静态库

弄清什么时候转码,什么时候不转码

### 导入流程

1. 将表格保存到应用服务磁盘的临时文件目录
2. 使用excel组件从磁盘中将其读到内存中
3. 逐行解析数据，构建成对应的DTO或DO
4. 保存到数据库中，注意此处是批量操作，在service中要开启事务
5. 保存成功后删除临时目录的报表(磁盘中的)
6. 保存响应结果

### 导出流程

(有相应的数据查询条件)

1. 验证查询条件
2. 根据条件获取数据
3. 将数据保存到excel文件中,并保存到磁盘的临时目录
4. 上传报表到FastDFS中
5. 下发文件下载地址



## 生成式服务



## 分层领域规约

### 领域对象描述

- `DO`(Data Object): 此对象与数据库表结构一一对应,通过`DAO`层向上传输数据源对象
- `DTO`(Data Transfer Object): 数据传输对象,Service 或 Manager 向外传输的对象
- `BO`(Business Object): 业务对象,可以由Service 层输出的封装业务逻辑对象
- `Query`: 数据查询对象,各层接受上层的查询请求.注意超过2个参数的查询封装,禁止使用Map类来进行传输
- `VO`(View Object): 显示层对象,通常是 Web 向模板渲染引擎层传输的对象

各层之间的关系如下图所示,包含了领域模型的传递过程

![分层领域规约](F:\project\zero-one-hrsys-1.0.0\hr-cpp\imgs\分层领域规约.png)
