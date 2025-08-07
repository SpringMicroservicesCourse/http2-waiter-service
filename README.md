我來為您撰寫 HTTP/2 微服務專案的 README 文件。

# HTTP/2 微服務架構實戰 ⚡

[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.2.5-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![HTTP/2](https://img.shields.io/badge/HTTP%2F2-Enabled-blue.svg)](https://http2.github.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 專案介紹

本專案展示如何在 Spring Boot 微服務架構中實作 HTTP/2 協議，包含服務端（Waiter Service）和客戶端（Customer Service）的完整實作範例。透過實際的咖啡訂單系統，演示現代微服務間的高效通信方式。

**核心功能**
- HTTP/2 協議的服務端與客戶端實作
- SSL/TLS 安全連接配置
- JPA 資料持久化與貨幣處理
- RESTful API 設計與實作
- 微服務間的安全通信

**解決問題**
- 提升微服務間通信效率
- 確保服務間通信的安全性
- 展示現代 Spring Boot 最佳實踐

**目標使用者**
- 微服務架構開發者
- Spring Boot 學習者
- HTTP/2 協議實作者

> �� **為什麼選擇此專案？**
> - 完整的 HTTP/2 微服務實作範例
> - 符合台灣本地化需求的貨幣處理
> - 清晰的程式碼結構與註解
> - 實用的 Maven 依賴管理最佳實踐

### 🎯 專案特色

- **HTTP/2 原生支援**：使用 Spring Boot 3.x 的 HTTP/2 功能
- **SSL/TLS 安全連接**：完整的憑證配置與安全通信
- **台灣本地化**：使用 TWD 貨幣與中文註解
- **最佳實踐**：統一的 Maven 依賴管理與程式碼結構
- **完整測試**：包含單元測試與整合測試

## 技術棧

### 核心框架
- **Spring Boot 3.2.5** - 現代化 Java 應用程式框架
- **Spring Data JPA** - 資料持久化與 ORM 映射
- **Spring Web** - RESTful API 開發
- **Spring Cache** - 快取機制支援

### 開發工具與輔助
- **OkHttp 4.12.0** - HTTP/2 客戶端庫
- **Joda Money 2.0.2** - 貨幣處理與計算
- **Apache Commons Lang3** - 工具類庫
- **Lombok** - 減少樣板程式碼
- **H2 Database** - 內嵌式資料庫

## 專案結構

```
http2-microservices/
├── http2-waiter-service/          # 服務端應用程式
│   ├── src/main/java/tw/fengqing/spring/springbucks/waiter/
│   │   ├── controller/            # REST API 控制器
│   │   ├── model/                 # 資料模型與實體
│   │   ├── repository/            # 資料存取層
│   │   ├── service/               # 業務邏輯層
│   │   └── support/               # 支援類別
│   └── src/main/resources/
│       ├── application.properties # 應用程式配置
│       ├── schema.sql            # 資料庫結構
│       └── data.sql              # 初始資料
├── http2-customer-service/        # 客戶端應用程式
│   ├── src/main/java/tw/fengqing/spring/springbucks/customer/
│   │   ├── model/                # 資料模型
│   │   └── support/              # 支援類別
│   └── src/main/resources/
│       └── application.properties # 客戶端配置
└── README.md
```

## 快速開始

### 前置需求
- Java 21 或以上版本
- Maven 3.6+ 建置工具
- Git 版本控制工具

### 安裝與執行

1. **克隆此倉庫：**
```bash
git clone https://github.com/SpringMicroservicesCourse/http2-microservices.git
```

2. **進入專案目錄：**
```bash
cd http2-waiter-service
```

3. **編譯服務端應用程式：**
```bash
cd http2-waiter-service
mvn clean compile
```

4. **執行服務端應用程式：**
```bash
mvn spring-boot:run
```

5. **編譯客戶端應用程式：**
```bash
cd ../http2-customer-service
mvn clean compile
```

6. **執行客戶端應用程式：**
```bash
mvn spring-boot:run
```

## 進階說明

### 環境變數
```properties
# 服務端配置 (waiter-service)
server.http2.enabled=true
server.port=8443
server.ssl.key-store=classpath:springbucks.p12
server.ssl.key-store-type=PKCS12
server.ssl.key-store-password=spring

# 客戶端配置 (customer-service)
waiter.service.url=https://localhost:8443
security.key-store=classpath:springbucks.p12
security.key-pass=spring
```

### 設定檔說明
```properties
# application.properties 主要設定
spring.jpa.hibernate.ddl-auto=none
spring.jpa.properties.hibernate.show_sql=true
management.endpoints.web.exposure.include=*
```

## API 端點說明

### 服務端 API (Waiter Service)

| 端點 | 方法 | 說明 | 範例 |
|------|------|------|------|
| `/coffee/` | GET | 取得所有咖啡清單 | `curl -k https://localhost:8443/coffee/` |
| `/coffee/{id}` | GET | 取得特定咖啡資訊 | `curl -k https://localhost:8443/coffee/1` |
| `/coffee/` | POST | 新增咖啡項目 | `curl -k -X POST https://localhost:8443/coffee/` |
| `/order/` | POST | 建立訂單 | `curl -k -X POST https://localhost:8443/order/` |
| `/order/{id}` | GET | 查詢訂單狀態 | `curl -k https://localhost:8443/order/1` |

### 測試指令
```bash
# 測試 HTTP/2 協議
curl -k -I https://localhost:8443/coffee/1

# 取得咖啡資訊
curl -k https://localhost:8443/coffee/1

# 查看詳細 HTTP/2 資訊
curl -k -v https://localhost:8443/coffee/1
```

## 參考資源

- [Spring Boot HTTP/2 官方文件](https://docs.spring.io/spring-boot/docs/current/reference/html/web.html#web.http2)
- [HTTP/2 協議規範](https://http2.github.io/)
- [OkHttp 官方文件](https://square.github.io/okhttp/)
- [Joda Money 貨幣處理](https://www.joda.org/joda-money/)

## 注意事項與最佳實踐

### ⚠️ 重要提醒

| 項目 | 說明 | 建議做法 |
|------|------|----------|
| SSL 憑證 | 開發環境使用自簽憑證 | 生產環境使用正式憑證 |
| HTTP/2 支援 | 確認客戶端支援 | 使用 curl 或現代瀏覽器測試 |
| 貨幣處理 | 避免浮點數計算 | 使用 Joda Money 進行精確計算 |
| 依賴管理 | 版本衝突處理 | 使用 dependencyManagement 統一管理 |

### �� 最佳實踐指南

- **Maven 依賴管理**：使用 `dependencyManagement` 統一管理版本
- **程式碼註解**：重要程式碼區塊添加清楚的中文註解
- **錯誤處理**：實作完整的例外處理機制
- **安全性**：使用 HTTPS 進行所有通信
- **效能優化**：啟用 HTTP/2 多路復用功能

### 💡 開發技巧

```java
// 貨幣處理最佳實踐
@Convert(converter = MoneyConverter.class)
private Money price;

// HTTP/2 客戶端配置
@Bean
public ClientHttpRequestFactory requestFactory() {
    OkHttpClient okHttpClient = new OkHttpClient.Builder()
        .sslSocketFactory(sslContext.getSocketFactory(), 
                         (X509TrustManager) tmf.getTrustManagers()[0])
        .hostnameVerifier((hostname, session) -> true)
        .build();
    return new OkHttp3ClientHttpRequestFactory(okHttpClient);
}
```

## 授權說明

本專案採用 MIT 授權條款，詳見 LICENSE 檔案。

## 關於我們

我們主要專注在敏捷專案管理、物聯網（IoT）應用開發和領域驅動設計（DDD）。喜歡把先進技術和實務經驗結合，打造好用又靈活的軟體解決方案。

## 聯繫我們

- **FB 粉絲頁**：[風清雲談 | Facebook](https://www.facebook.com/profile.php?id=61576838896062)
- **LinkedIn**：[linkedin.com/in/chu-kuo-lung](https://www.linkedin.com/in/chu-kuo-lung)
- **YouTube 頻道**：[雲談風清 - YouTube](https://www.youtube.com/channel/UCXDqLTdCMiCJ1j8xGRfwEig)
- **風清雲談 部落格**：[風清雲談](https://blog.fengqing.tw/)
- **電子郵件**：[fengqing.tw@gmail.com](mailto:fengqing.tw@gmail.com)

---

**📅 最後更新：2025-08-07**  
**👨‍💻 維護者：風清雲談團隊**