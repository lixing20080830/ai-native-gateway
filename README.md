# ai-native-gateway

一个基于 Spring Cloud Gateway（WebFlux）和 Nacos 服务发现的简单网关示例。

## 环境要求

- JDK 17+
- Maven 3.6+
- Nacos Server
- 一个已注册到相同 Nacos namespace 的 `user-service`

## 启动

默认连接 `127.0.0.1:8848`：

```bash
mvn spring-boot:run
```

也可以通过环境变量配置 Nacos 地址和 namespace：

```bash
NACOS_ADDR=127.0.0.1:8848 NACOS_NAMESPACE=public mvn spring-boot:run
```

Windows PowerShell 示例：

```powershell
$env:NACOS_ADDR = "127.0.0.1:8848"
$env:NACOS_NAMESPACE = "public"
mvn spring-boot:run
```

网关监听 `8080` 端口并注册到 Nacos。访问 `http://localhost:8080/api/users/123` 时，网关通过 Nacos 发现 `user-service` 实例并转发请求。`StripPrefix=1` 会在转发前去掉 `/api` 前缀，因此后端收到的路径为 `/users/123`。

确保 `user-service` 的服务名、namespace 与网关一致。依赖版本集中定义在 `pom.xml`，如需更换版本，请按 Spring Cloud Alibaba 官方兼容矩阵同步调整 Spring Boot、Spring Cloud 和 Spring Cloud Alibaba 版本。
