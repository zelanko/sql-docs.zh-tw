---
title: JDBC Driver 常見問題集 (FAQ)| Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cbc0e397-ecf2-4494-87b2-a492609bceae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cb77bd5ac3ccc2e12dd7fbf9aff956981b25bce3
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/05/2019
ms.locfileid: "55737049"
---
# <a name="frequently-asked-questions-faq-for-jdbc-driver"></a>JDBC Driver 常見問題集 (FAQ)

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

此頁面提供有關 Microsoft JDBC Driver for SQL Server 之常見問題的答案。

## <a name="frequently-asked-questions"></a>常見問題集

**如何協助改善 JDBC 驅動程式？**  
JDBC 驅動程式是開放原始碼，而且可以找到的原始程式碼[GitHub](https://github.com/microsoft/mssql-jdbc)。 您可以協助改善驅動程式所提出的問題，並且積極參與程式碼基底。

**此驅動程式支援哪些版本的 SQL Server 及 Java？**  
如需詳細資，請參閱 [Microsoft JDBC Driver for SQL Server 支援對照表](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md)頁面。

**什麼是 Microsoft Download Center 上可用的 JDBC 驅動程式套件與 JDBC 驅動程式可在 GitHub 上的差異？**  
JDBC 驅動程式檔案可以使用 GitHub 存放庫上的 Microsoft JDBC driver 是 JDBC 驅動程式的核心，在存放庫中列出的開放原始碼授權下。 在 Microsoft 下載中心上的驅動程式套件包含適用於 Windows 整合式驗證和透過 JDBC 驅動程式的啟用 XA 交易的其他程式庫。 這些額外的程式庫是可下載的套件所隨附的授權。

**升級我的驅動程式前，我應該先知道哪些事？**
Microsoft JDBC Driver 7.2 支援 JDBC 4.2 和 4.3 （部分） 規格，並在安裝套件包含兩個 JAR 類別庫時，也將，如下所示：

| JAR                        | JDBC 規格            | JDK 版本 |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.2.0.jre11.jar | JDBC 4.3 （部分），和 4.2 | JDK 11.0    |
| mssql-jdbc-7.2.0.jre8.jar  | JDBC 4.2                      | JDK 8.0     |

 Microsoft JDBC Driver 7.0 支援 JDBC 4.2 和 4.3 （部分） 規格，並在安裝套件包含兩個 JAR 類別庫時，也將，如下所示：

| JAR                        | JDBC 規格            | JDK 版本 |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.0.0.jre10.jar | JDBC 4.3 （部分），和 4.2 | JDK 10.0    |
| mssql-jdbc-7.0.0.jre8.jar  | JDBC 4.2                      | JDK 8.0     |

Microsoft JDBC Driver 6.4 支援 JDBC 4.1、 4.2、 和 4.3 （部分） 規格和三個 JAR 類別庫納入安裝套件，如下所示：

| JAR                       | JDBC 規格                 | JDK 版本 |
| ------------------------- | ---------------------------------- | ----------- |
| mssql-jdbc-6.4.0.jre9.jar | JDBC 4.3 （部分）、 4.2 與 4.1 | JDK 9.0     |
| mssql-jdbc-6.4.0.jre8.jar | JDBC 4.2 與 4.1                  | JDK 8.0     |
| mssql-jdbc-6.4.0.jre7.jar | JDBC 4.1                           | JDK 7.0     |

Microsoft JDBC Driver 6.2 支援 JDBC 4.0、 4.1 和 4.2 規格，並在安裝套件包含兩個 JAR 類別庫時，也將，如下所示：

| JAR                       | JDBC 規格     | JDK 版本 |
| ------------------------- | ---------------------- | ----------- |
| mssql-jdbc-6.2.2.jre8.jar | JDBC 4.2、4.1 及 4.0 | JDK 8.0     |
| mssql-jdbc-6.2.2.jre7.jar | JDBC 4.1 及 4.0       | JDK 7.0     |

Microsoft JDBC Drivers 6.0 與 4.2 for SQL Server 支援 JDBC 4.0、 4.1 和 4.2 規格，並在安裝套件中包含兩個 JAR 類別庫時，也將，如下所示：

| JAR           | JDBC 規格     | JDK 版本 |
| ------------- | ---------------------- | ----------- |
| sqljdbc42.jar | JDBC 4.2、4.1 及 4.0 | JDK 8.0     |
| sqljdbc41.jar | JDBC 4.1 及 4.0       | JDK 7.0     |

Microsoft JDBC Driver 4.1 for SQL Server 支援 JDBC 4.0 規格，並在安裝套件中包含一個 JAR 類別庫時，也將，如下所示：

| JAR           | JDBC 規格 | JDK 版本     |
| ------------- | ------------------ | --------------- |
| sqljdbc41.jar | JDBC 4.0           | JDK 7.0 與 6.0 |

**若我想要在現有的 SQL Server 版本上使用最新版的驅動程式，我需要變更應用程式的任何程式碼嗎？**  
一般而言，驅動程式的設計具有回溯相容功能，因此當您升級驅動程式時，並不需要變更現有的應用程式。 新的驅動程式版本導入重大變更， [JDBC 驅動程式的版本資訊](../../connect/jdbc/release-notes-for-the-jdbc-driver.md)區段提供清楚的詳細資料變更，而且對現有的應用程式的影響。 此外，您也可以檢閱驅動程式隨附的版本資訊，查看該版本中已經修正之錯誤與已知問題的清單。

**此驅動程式的售價為何？**  
Microsoft JDBC Driver for SQL Server 為免費提供。

**我可以轉散發此驅動程式嗎？**
JDBC Driver 4.1/4.2、 6.0、 6.2、 6.4、 / 7.0 是可轉散發套件。 檢閱授權合約的 「 可散發程式碼 」 子句。

**我可以使用此驅動程式從 Linux 電腦存取 Microsoft SQL Server 嗎？**
當然可以。 您可以使用此驅動程式從 Linux、 Unix 及其他非 Windows 平台存取 SQL Server。 如需詳細資訊，請參閱 < [Microsoft JDBC Driver for SQL Server Support Matrix](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md)。

**此驅動程式支援安全通訊端層 (SSL) 加密嗎？**
此驅動程式自 1.2 版起，即支援安全通訊端層 (SSL) 加密。 如需詳細資訊，請參閱 [使用 SSL 加密](../../connect/jdbc/using-ssl-encryption.md)。

**Microsoft JDBC Driver for SQL Server 支援哪些驗證類型？**  
下表列出可用的驗證選項。 只有 4.0 版以後的驅動程式，才能使用純 Java Kerberos 驗證。

|             |                                       |
| ----------- | ------------------------------------- |
| 平台    | 驗證                        |
| 非 Windows | 純 Java Kerberos                    |
| 非 Windows | [SQL Server]                            |
| 非 Windows | Azure Active Directory 驗證 |
| Windows     | 純 Java Kerberos                    |
| Windows     | [SQL Server]                            |
| 視窗     | Kerberos 加 NTLM 備份             |
| Windows     | NTLM                                  |
| Windows     | Azure Active Directory 驗證 |

**此驅動程式支援網際網路通訊協定第 6 版 (IPv6) 位址嗎？**  
是的。 驅動程式支援使用 IPv6 位址。 使用連接屬性集合和 serverName 連接字串屬性。 如需詳細資訊，請參閱[建置連線 URL](../../connect/jdbc/building-the-connection-url.md)。

**什麼是自適性緩衝？**  
適應性緩衝是從 Microsoft SQL Server 2005 JDBC Driver 1.2 版引進。 它是針對在沒有伺服器資料指標負擔的情況下，擷取任何種類的大數值資料而設計的。 Microsoft SQL Server JDBC Driver 的自適性緩衝功能提供連接字串屬性 responseBuffering，可以設定為 "adaptive" 或 "full"。 在 1.2 版中，預設的緩衝模式為 "full"，而且應用程式必須明確自適性緩衝模式。 自 JDBC Driver 2.0 版起，此驅動程式的預設行為是 "adaptive"。 因此，您的應用程式不需要明確要求自適性行為，就能取得自適性緩衝行為。 如需詳細資訊，請參閱[使用自適性緩衝](../../connect/jdbc/using-adaptive-buffering.md)與 [What is adaptive response buffering and why should I use it?](https://go.microsoft.com/fwlink/?LinkId=111575) (什麼是自適性回應緩衝，以及我為何應該使用它？) 部落格。

**此驅動程式支援連線共用嗎？**  
此驅動程式提供支援 Java Platform, Enterprise Edition 5 (Java EE 5) 的連接共用。 此驅動程式實作了 JDBC 3.0 所需的介面，讓驅動程式能夠參與中介軟體應用程式廠商所提供的連接共用實作。 此驅動程式可參與這些環境中的共用連接。 如需詳細資訊，請參閱 [Using Connection Pooling](../../connect/jdbc/using-connection-pooling.md)。 此驅動程式不提供自己的共用實作，而會使用第三方 Java 應用程式伺服器。

**此驅動程式是否提供任何支援選項？**  
此驅動程式提供數個支援選項。 您可以張貼您的問題，或發出給我們[GitHub 存放庫](https://github.com/microsoft/mssql-jdbc)這由 Microsoft 監視。 [論壇](https://go.microsoft.com/fwlink/?LinkID=246673)受 Microsoft、 Mvp 和社群。 您也可以連絡 Microsoft 客戶支援服務。 開發小組可能會要求您重現任何第三方應用程式伺服器以外的問題。 若無法在裝載 Java 容器之環境以外之處重現問題，您必須連絡相關的第三方廠商，小組才能繼續協助您。 小組可能也會要求您重新產生您的問題，例如 Windows 作業系統上，因此可以最佳支援問題。

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

[JDBC Driver 概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)
