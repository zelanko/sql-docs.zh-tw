---
title: JDBC 驅動程式常見問題集 (FAQ) | Microsoft Docs
ms.custom: ''
ms.date: 01/29/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cbc0e397-ecf2-4494-87b2-a492609bceae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1055b9b0422073d7b9875c748dcfe889af053dc2
ms.sourcegitcommit: 4b2c9d648b7a7bdf9c3052ebfeef182e2f9d66af
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/04/2020
ms.locfileid: "77004627"
---
# <a name="frequently-asked-questions-faq-for-jdbc-driver"></a>JDBC 驅動程式常見問題集 (FAQ)

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

此頁面提供有關 Microsoft JDBC Driver for SQL Server 之常見問題的答案。

## <a name="frequently-asked-questions"></a>常見問題集

**如何協助改進 JDBC Driver？**  
JDBC Driver 是開放原始碼，您可以在 [GitHub](https://github.com/microsoft/mssql-jdbc) \(英文\) 上找到原始程式碼。 您可以藉由提出問題並參與程式碼基底來協助改進此驅動程式。

**此驅動程式支援哪些版本的 SQL Server 及 Java？**  
如需詳細資訊，請參閱[適用於 SQL Server 的 Microsoft JDBC 驅動程式支援對照表](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md)頁面。

**Microsoft 下載中心提供的 JDBC 驅動程式套件與 GitHub 上提供的 JDBC 驅動程式有何差異？**  
GitHub 存放庫上針對 Microsoft JDBC 驅動程式提供的 JDBC 驅動程式檔案為 JDBC 驅動程式的核心，且屬於存放庫中列出的開放原始碼授權。 Microsoft 下載中心的驅動程式套件包含適用於 Windows 整合式驗證及透過 JDBC 驅動程式啟用 XA 交易的額外程式庫。 那些額外的程式庫均屬於可下載套件隨附的授權。

**升級我的驅動程式前，我應該先知道哪些事？**  
Microsoft JDBC Driver 8.2 支援 JDBC 4.2 和 4.3 (部分) 規格，同時也在安裝套件中包含下列三個 JAR 類別庫：

| JAR                        | JDBC 規格            | JDK 版本 |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-8.2.0.jre13.jar | JDBC 4.3 (部份) 和 4.2 | JDK 13.0    |
| mssql-jdbc-8.2.0.jre11.jar | JDBC 4.3 (部份) 和 4.2 | JDK 11.0    |
| mssql-jdbc-8.2.0.jre8.jar  | JDBC 4.2                      | JDK 8.0     |
| &nbsp;                     | &nbsp;                        | &nbsp;      |

Microsoft JDBC Driver 7.4 支援 JDBC 4.2 和 4.3 (部份) 規格，同時也在安裝套件中包含了下列三個 JAR 類別庫：

| JAR                        | JDBC 規格            | JDK 版本 |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.4.1.jre12.jar | JDBC 4.3 (部份) 和 4.2 | JDK 12.0    |
| mssql-jdbc-7.4.1.jre11.jar | JDBC 4.3 (部份) 和 4.2 | JDK 11.0    |
| mssql-jdbc-7.4.1.jre8.jar  | JDBC 4.2                      | JDK 8.0     |
| &nbsp;                     | &nbsp;                        | &nbsp;      |

Microsoft JDBC Driver 7.2 支援 JDBC 4.2 與 4.3 (部份) 規格，同時也在安裝套件中包含了下列兩個 JAR 類別庫：

| JAR                        | JDBC 規格            | JDK 版本 |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.2.2.jre11.jar | JDBC 4.3 (部份) 和 4.2 | JDK 11.0    |
| mssql-jdbc-7.2.2.jre8.jar  | JDBC 4.2                      | JDK 8.0     |
| &nbsp;                     | &nbsp;                        | &nbsp;      |

Microsoft JDBC Driver 7.0 支援 JDBC 4.2 與 4.3 (部份) 規格，同時也在安裝套件中包含了下列兩個 JAR 類別庫：

| JAR                        | JDBC 規格            | JDK 版本 |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.0.0.jre10.jar | JDBC 4.3 (部份) 和 4.2 | JDK 10.0    |
| mssql-jdbc-7.0.0.jre8.jar  | JDBC 4.2                      | JDK 8.0     |
| &nbsp;                     | &nbsp;                        | &nbsp;      |

Microsoft JDBC Driver 6.4 支援 JDBC 4.1、4.2 及 4.3 (部份) 規格，同時也在安裝套件中包含了下列三個 JAR 類別庫：

| JAR                       | JDBC 規格                 | JDK 版本 |
| ------------------------- | ---------------------------------- | ----------- |
| mssql-jdbc-6.4.0.jre9.jar | JDBC 4.3 (部份)、4.2 及 4.1 | JDK 9.0     |
| mssql-jdbc-6.4.0.jre8.jar | JDBC 4.2 與 4.1                  | JDK 8.0     |
| mssql-jdbc-6.4.0.jre7.jar | JDBC 4.1                           | JDK 7.0     |
| &nbsp;                    | &nbsp;                             | &nbsp;      |

Microsoft JDBC Driver 6.2 支援 JDBC 4.0、4.1 及 4.2 規格，同時也在安裝套件中包含了下列兩個 JAR 類別庫：

| JAR                       | JDBC 規格     | JDK 版本 |
| ------------------------- | ---------------------- | ----------- |
| mssql-jdbc-6.2.2.jre8.jar | JDBC 4.2、4.1 及 4.0 | JDK 8.0     |
| mssql-jdbc-6.2.2.jre7.jar | JDBC 4.1 及 4.0       | JDK 7.0     |
| &nbsp;                    | &nbsp;                 | &nbsp;      |

Microsoft JDBC Driver 6.0 和 4.2 for SQL Server支援 JDBC 4.0、4.1 及 4.2 規格，同時也在安裝套件中包含了下列兩個 JAR 類別庫：

| JAR           | JDBC 規格     | JDK 版本 |
| ------------- | ---------------------- | ----------- |
| sqljdbc42.jar | JDBC 4.2、4.1 及 4.0 | JDK 8.0     |
| sqljdbc41.jar | JDBC 4.1 及 4.0       | JDK 7.0     |
| &nbsp;        | &nbsp;                 | &nbsp;      |

Microsoft JDBC Driver 4.1 for SQL Server 支援 JDBC 4.0 規格，同時也在安裝套件中包含了下列這一個 JAR 類別庫：

| JAR           | JDBC 規格 | JDK 版本     |
| ------------- | ------------------ | --------------- |
| sqljdbc41.jar | JDBC 4.0           | JDK 7.0 與 6.0 |
| &nbsp;        | &nbsp;             | &nbsp;      |

**若我想要在現有的 SQL Server 版本上使用最新版的驅動程式，我需要變更應用程式的任何程式碼嗎？**  
一般而言，驅動程式的設計具有回溯相容功能，因此當您升級驅動程式時，並不需要變更現有的應用程式。 新驅動程式版本如有引進重大變更，就會在 [JDBC Driver 的版本資訊](../../connect/jdbc/release-notes-for-the-jdbc-driver.md)一節中詳細說明這類變更，以及變更對於現有應用程式的影響。 此外，您也可以檢閱驅動程式隨附的版本資訊，查看該版本中已經修正之錯誤與已知問題的清單。

**此驅動程式的售價為何？**  
Microsoft JDBC Driver for SQL Server 為免費提供。

**我可以轉散發此驅動程式嗎？**  
JDBC 驅動程式 6.0、6.2、6.4 與 7.0 是可轉發的。 請檢閱授權合約中的「可轉散發程式碼」條款。

**我可以使用此驅動程式從 Linux 電腦存取 Microsoft SQL Server 嗎？**  
可以！ 您可以使用此驅動程式從 Linux、 Unix 及其他非 Windows 平台存取 SQL Server。 如需詳細資料，請參閱 [Microsoft JDBC Driver for SQL Server 支援對照表](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md)。

**此驅動程式支援安全通訊端層 (SSL) 加密嗎？**  
此驅動程式自 1.2 版起，即支援安全通訊端層 (SSL) 加密。 如需詳細資訊，請參閱 [使用 SSL 加密](../../connect/jdbc/using-ssl-encryption.md)。

**Microsoft JDBC Driver for SQL Server 支援哪些驗證類型？**  
下表列出可用的驗證選項。 只有 4.0 版以後的驅動程式，才能使用純 Java Kerberos 驗證。

| 平台    | 驗證                        |
| ----------- | ------------------------------------- |
| 非 Windows | 純 Java Kerberos                    |
| 非 Windows | SQL Server                            |
| 非 Windows | Azure Active Directory 驗證 |
| Windows     | 純 Java Kerberos                    |
| Windows     | SQL Server                            |
| Windows     | Kerberos 加 NTLM 備份             |
| Windows     | NTLM                                  |
| Windows     | Azure Active Directory 驗證 |
| &nbsp;      | &nbsp;                                |

**此驅動程式支援網際網路通訊協定第 6 版 (IPv6) 位址嗎？**  
是。 此驅動程式支援使用 IPv6 位址。 使用連線屬性集合和 serverName 連接字串屬性。 如需詳細資訊，請參閱[建置連線 URL](../../connect/jdbc/building-the-connection-url.md)。

**什麼是自適性緩衝？**  
自適性緩衝是從 Microsoft SQL Server 2005 JDBC Driver 1.2 版開始引進的。 它是針對在沒有伺服器資料指標負擔的情況下，擷取任何種類的大數值資料而設計的。 Microsoft SQL Server JDBC Driver 的自適性緩衝功能提供連接字串屬性 responseBuffering，可以設定為 "adaptive" 或 "full"。 在 1.2 版中，預設的緩衝模式為 "full"，而且應用程式必須明確自適性緩衝模式。 自 JDBC Driver 2.0 版起，此驅動程式的預設行為是 "adaptive"。 因此，您的應用程式不需要明確要求自適性行為，就能取得自適性緩衝行為。 如需詳細資訊，請參閱[使用自適性緩衝](../../connect/jdbc/using-adaptive-buffering.md)與 [What is adaptive response buffering and why should I use it?](https://go.microsoft.com/fwlink/?LinkId=111575) (什麼是自適性回應緩衝，以及我為何應該使用它？) 部落格。

**此驅動程式支援連線共用嗎？**  
此驅動程式提供支援 Java Platform, Enterprise Edition 5 (Java EE 5) 的連接共用。 此驅動程式實作了 JDBC 3.0 所需的介面，讓驅動程式能夠參與中介軟體應用程式廠商所提供的連接共用實作。 此驅動程式可參與這些環境中的共用連接。 如需詳細資訊，請參閱[使用連線共用](../../connect/jdbc/using-connection-pooling.md)。 此驅動程式不提供自己的共用實作，而會使用第三方 Java 應用程式伺服器。

**此驅動程式是否提供任何支援選項？**  
此驅動程式提供數個支援選項。 您可以在我們的 [GitHub 存放庫](https://github.com/microsoft/mssql-jdbc) \(英文\) 上張貼或提出問題，這會由 Microsoft 監控。 [論壇](https://go.microsoft.com/fwlink/?LinkID=246673) \(英文\) 會由 Microsoft、MVP 和社群監控。 您也可以連絡 Microsoft 客戶支援服務。 開發小組可能會要求您重現任何第三方應用程式伺服器以外的問題。 若無法在裝載 Java 容器之環境以外之處重現問題，您必須連絡相關的第三方廠商，小組才能繼續協助您。 該小組也可能要求您在作業系統 (例如 Windows) 上重現您的問題，以便為該問題提供最佳支援。

**此驅動程式是否通過認證，可與任何第三方應用程式伺服器搭配使用？**  
此驅動程式已在多種應用程式伺服器上進行過測試，包括 IBM WebSphere 及 SAP NetWeaver。

**如何啟用追蹤功能？**  
此驅動程式支援追蹤 (或記錄) 功能，可用於協助解決在應用程式中使用 JDBC 驅動程式時所發生的問題。 為能在用戶端上使用 JAR 追蹤，JDBC 驅動程式會使用 java.util.logging 中的記錄 API java.util.logging。 如需詳細資訊，請參閱[追蹤驅動程式作業](../../connect/jdbc/tracing-driver-operation.md)。 對於伺服器端的 XA 追蹤，請參閱 [Data Access Tracing in SQL Server](https://go.microsoft.com/fwlink/?LinkId=248705)(SQL Server 的資料存取追蹤)。

**何處可以下載舊版的驅動程式？例如 SQL Server 2000 的 JDBC 驅動程、2005 驅動程式、1.0、1.1 或 1.2 版的驅動程式。**  
因為已經停止支援這些驅動程式版本，所以也不再提供其下載。 因為我們會持續改進 Java 連線能力支援， 所以極力建議您使用最新版的 Microsoft JDBC 驅動程式。

**我使用 JRE 1.4。哪一個驅動程式與 JRE 1.4 相容？**  
對於使用 SAP 產品並需要 JRE 1.4 支援的客戶，請連絡 [SAPService Marketplace](https://service.sap.com/) ，以取得 1.2 Microsoft JDBC Driver。

**此驅動程式可以使用 FIPS 驗證演算法進行通訊嗎？**  
Microsoft JDBC Driver 不含任何密碼編譯演算法。 若客戶使用作業系統、應用程式及聯邦資訊處理標準 (FIPS) 可接受的 JVM 演算法，並將驅動程式設定成使用這些演算法，則此驅動程式只會使用指定的演算法進行通訊。

## <a name="see-also"></a>另請參閱

[JDBC 驅動程式概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)
