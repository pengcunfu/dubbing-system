# DubbingSystem 配音助手

基于 SpringBoot + Vue 开发的多人在线协作 AI 配音工具

## 项目简介

DubbingSystem（魔音配音助手）是一个企业级的在线配音系统，集成了多个主流语音合成 API，为用户提供高质量的文本转语音服务。系统采用前后端分离架构，支持 SSML 语法标记，提供丰富的配音参数控制。

**主要集成服务：**
- 魔音工坊开放平台 API
- 讯飞语音合成 API
- 百度语音合成 API
- 百度语音识别 API

> 注：目前主要实现了魔音工坊 API 接口服务的调用

## 技术栈

### 后端技术
- **框架**: Spring Boot 2.5.15
- **数据库**: MySQL 8.0
- **缓存**: Redis 3.0+
- **JDK**: 1.8
- **构建工具**: Maven
- **API 文档**: Swagger 3.0
- **任务调度**: Quartz
- **权限框架**: Spring Security + JWT

### 前端技术

**管理后台 (moyin-admin)**
- Vue 2.6.12
- Element UI 2.15.13
- Vuex 3.6.0
- Vue Router 3.4.9
- Axios 0.24.0

**用户前台 (moyin-user)**
- Vue 3.4.12
- TypeScript 5.1.6
- Vite 4.4.6
- Pinia 2.1.6
- Element Plus 2.3.12
- SSML Editor (基于 wangeditor)

### 部署技术
- Docker & Docker Compose
- Nginx (反向代理)

## 项目结构

```
dubbing-system/
├── moyin-server/              # 后端服务（Spring Boot）
│   ├── moyin-admin/          # 管理后台模块
│   ├── moyin-api/            # API 接口模块
│   ├── moyin-common/         # 通用工具模块
│   ├── moyin-framework/      # 框架核心模块
│   ├── moyin-generator/      # 代码生成器
│   ├── moyin-quartz/         # 定时任务模块
│   ├── moyin-system/         # 系统管理模块
│   └── sql/                  # 数据库脚本
├── moyin-admin/              # 管理后台前端（Vue2 + Element UI）
│   ├── src/
│   │   ├── api/             # API 接口
│   │   ├── views/           # 页面组件
│   │   ├── components/      # 公共组件
│   │   ├── router/          # 路由配置
│   │   └── store/           # Vuex 状态管理
│   └── public/
├── moyin-user/               # 用户前台（Vue3 + TypeScript + Vite）
│   ├── src/
│   │   ├── api/             # API 接口
│   │   ├── views/           # 页面视图
│   │   ├── components/      # 公共组件
│   │   ├── core/            # 核心功能模块
│   │   ├── menu/            # 菜单配置
│   │   ├── stores/          # Pinia 状态管理
│   │   └── router/          # 路由配置
│   └── public/
├── moyin-deploy/             # 部署脚本工具
│   ├── compile/             # 编译脚本
│   ├── deploy/              # 部署脚本
│   └── maintain/            # 维护脚本
├── docker/                   # Docker 配置
│   ├── docker-compose.yml   # Docker Compose 配置
│   ├── nginx/               # Nginx 配置
│   ├── mysql/               # MySQL 配置
│   └── redis/               # Redis 配置
├── scripts/                  # 工具脚本
│   ├── build/               # 构建脚本
│   ├── deploy/              # 部署脚本
│   └── data_maintenance/    # 数据维护脚本
└── docs/                     # 项目文档
```

## 环境要求

### 开发环境
- **Node.js**: 16.13.0+
- **npm**: 8.1.2+
- **JDK**: 1.8+
- **Maven**: 3.6+
- **MySQL**: 8.0+
- **Redis**: 3.0+

### 推荐开发工具
- **后端**: IntelliJ IDEA
- **前端**: VS Code
- **数据库**: Navicat / DBeaver
- **API 测试**: Postman

## 快速开始

### 1. 克隆项目
```bash
git clone <repository-url>
cd dubbing-system
```

### 2. 数据库初始化
```bash
# 导入数据库脚本
mysql -u root -p < moyin-server/sql/dubbing_sys.sql
```

### 3. 配置文件修改

**后端配置** (`moyin-server/moyin-admin/src/main/resources/application.yml`):
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/dubbing_sys?useUnicode=true&characterEncoding=utf8&serverTimezone=Asia/Shanghai
    username: root
    password: your_password
  redis:
    host: localhost
    port: 6379
    password: your_redis_password
```

**前端配置**:
- 管理后台: `moyin-admin/vue.config.js`
- 用户前台: `moyin-user/vite.config.ts`

### 4. 后端启动

```bash
cd moyin-server
mvn clean install
cd moyin-admin
mvn spring-boot:run
```

或使用 IDEA 直接运行 `moyin-admin` 模块的启动类。

默认访问地址: `http://localhost:8080`

### 5. 前端启动

**管理后台**:
```bash
cd moyin-admin
npm install
npm run dev
```
访问地址: `http://localhost:80`

**用户前台**:
```bash
cd moyin-user
npm install
npm run dev
```
访问地址: `http://localhost:5793`

## 项目部署

### 方式一：传统部署

**1. 前端打包**
```bash
# 打包管理后台
cd moyin-admin
npm run build:prod

# 打包用户前台
cd moyin-user
npm run build-only
```

**2. 后端打包**
```bash
cd moyin-server
mvn clean package
```

**3. 部署到服务器**
- 将前端打包文件部署到 Nginx
- 将后端 jar 包部署到服务器并运行
- 配置 Nginx 反向代理

### 方式二：Docker 部署（推荐）

```bash
cd docker
docker-compose up -d
```

服务端口：
- Nginx (用户前台): `80`
- Nginx (管理后台): `81`
- MySQL: `33061`
- Redis: `63791`

### 方式三：使用部署脚本

```bash
cd moyin-deploy
npm install
npm run deploy
```

## 核心功能

### 已实现功能
- ✅ 文本转语音（TTS）
- ✅ SSML 语法支持
- ✅ 多发音人选择
- ✅ 语音参数调节（语速、音调、音量）
- ✅ 音频文件管理
- ✅ 用户权限管理
- ✅ 系统配置管理
- ✅ 操作日志记录

### 规划中功能
- 🔲 多人协作配音
- 🔲 语音识别（ASR）
- 🔲 音频编辑功能
- 🔲 批量配音任务
- 🔲 配音模板管理

## SSML 语法支持

系统支持以下 SSML 标签：

| 标签 | 功能 | 示例 |
|------|------|------|
| `<speak>` | SSML 根标签 | `<speak>文本内容</speak>` |
| `<voice>` | 指定发音人 | `<voice name="speaker1">文本</voice>` |
| `<prosody>` | 调节语速、音调、音量 | `<prosody rate="fast" pitch="high">文本</prosody>` |
| `<break>` | 插入停顿 | `<break time="500ms"/>` |
| `<emphasis>` | 强调 | `<emphasis level="strong">重要</emphasis>` |
| `<say-as>` | 指定朗读方式 | `<say-as interpret-as="telephone">12345</say-as>` |
| `<phoneme>` | 音标发音 | `<phoneme alphabet="py" ph="ni3 hao3">你好</phoneme>` |
| `<sub>` | 替换发音 | `<sub alias="人工智能">AI</sub>` |
| `<p>` / `<s>` | 段落/句子 | `<p>段落文本</p>` |
| `<w>` | 单词 | `<w>单词</w>` |
| `<audio>` | 插入音频 | `<audio src="url">替代文本</audio>` |
| `<mark>` | 标记 | `<mark name="mark1"/>` |

## API 文档

启动后端服务后，访问 Swagger API 文档：

```
http://localhost:8080/swagger-ui/index.html
```

## 数据库脚本维护

系统提供了数据维护脚本，位于 `scripts/data_maintenance/`:

- `import_moyin_speaker.py` - 导入发音人数据
- `import_moyin_language.py` - 导入语言数据
- `import_moyin_emotion.py` - 导入情感数据
- `import_moyin_age.py` - 导入年龄段数据
- `import_moyin_domain.py` - 导入领域数据
- `associated_moyin_speaker.py` - 关联发音人数据
- `speaker_batch_enable.py` / `speaker_batch_disable.py` - 批量启用/禁用发音人

## 开发指南

### 代码规范
- 后端遵循阿里巴巴 Java 开发规范
- 前端遵循 Vue 官方风格指南
- 提交前请运行 `npm run lint` 检查代码

### 分支管理
- `master` - 主分支（稳定版本）
- `develop` - 开发分支
- `feature/*` - 功能分支
- `hotfix/*` - 紧急修复分支

### 提交规范
```
feat: 新功能
fix: 修复问题
docs: 文档修改
style: 代码格式调整
refactor: 重构
test: 测试相关
chore: 构建/工具链修改
```

## 常见问题

### 1. 前端跨域问题
配置 `vue.config.js` 或 `vite.config.ts` 中的 proxy 代理。

### 2. 数据库连接失败
检查数据库配置、用户名密码、数据库是否启动。

### 3. Redis 连接失败
检查 Redis 配置、密码、端口是否正确。

### 4. 打包后静态资源 404
检查 Nginx 配置和前端 `publicPath` 配置。

## 贡献指南

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 提交 Pull Request

## 许可证

本项目基于 MIT 协议开源。

## 联系方式

如有问题，请提交 Issue 或联系项目维护者。

## 致谢

- [若依管理系统](http://www.ruoyi.vip/) - 后台管理框架
- [魔音工坊](https://www.moyin.com/) - 语音合成 API
- [wangeditor](https://www.wangeditor.com/) - 富文本编辑器

---

**⭐ 如果这个项目对你有帮助，请给一个 Star！**
