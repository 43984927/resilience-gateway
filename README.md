# Resilience-Gateway 🛡️

一款具备"自愈能力"和"混沌测试（Chaos Testing）"功能的轻量级 API 网关演示原型。

## 💡 设计思考 (Architecture Thoughts)

在长期保障电信级 CRM 核心系统高可用，以及处理跨境电商复杂网络环境的实战中，我深刻体会到：**系统的脆弱性往往暴露在网络抖动和流量突刺中。** 本项目旨在提供基础请求代理的同时，内置**故障模拟机制**，帮助开发与 QA 团队前置验证系统的熔断、降级与超时控制机制。

## 🚀 核心特性

- **轻量级转发**：基于 Java 17 + Spring Boot 3 构建。
- **混沌注入 (Chaos Injection)**：
  - `delayMs`：API 级别动态延迟注入（模拟跨国网络丢包/拥塞）。
  - `forceError`：强制错误注入（模拟底层数据库死锁或服务雪崩）。
- **自动化交付**：配置完整的 `Dockerfile` 与 `GitHub Actions`，实现代码提交即刻构建。

## 🛠️ 快速体验接口 (Live Demo)

*(注意：部署后将这里的链接替换为你的真实云端域名)*

1. **正常请求**: 
   `GET https://[你的域名]/api/v1/proxy`
2. **模拟跨境网络延迟 (500ms)**: 
   `GET https://[你的域名]/api/v1/proxy?delayMs=500`
3. **模拟底层服务熔断 (HTTP 500)**: 
   `GET https://[你的域名]/api/v1/proxy?forceError=true`

## 📦 容器化运行

```bash
docker build -t resilience-gateway .
docker run -d -p 8080:8080 resilience-gateway
```

## 🧪 本地开发

```bash
mvn spring-boot:run
```

## 📊 技术栈

- **语言**: Java 17
- **框架**: Spring Boot 3.2.3
- **构建工具**: Maven
- **容器化**: Docker Multi-stage Build
- **CI/CD**: GitHub Actions

## 🏗️ 项目结构

```
Resilience-Gateway/
├── .github/
│   └── workflows/
│       └── main.yml
├── src/
│   └── main/
│       ├── java/
│       │   └── com/
│       │       └── gateway/
│       │           ├── ResilienceGatewayApplication.java
│       │           └── controller/
│       │               └── GatewayController.java
│       └── resources/
│           └── application.properties
├── Dockerfile
├── pom.xml
└── README.md
```

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request！

## 📄 许可证

This project is licensed under the MIT License - see the LICENSE file for details.
