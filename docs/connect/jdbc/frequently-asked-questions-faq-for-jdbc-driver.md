---
title: "常見問題集 (FAQ) JDBC driver |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cbc0e397-ecf2-4494-87b2-a492609bceae
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 508f8526ed13af3f7f92aa500b182e077f5bb23d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="frequently-asked-questions-faq-for-jdbc-driver"></a>常見問題集 (FAQ) 的 JDBC 驅動程式
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  本文提供有關 Microsoft JDBC Driver for SQL Server 之常見問題的答案。  
  
## <a name="frequently-asked-questions"></a>常見問題集  
**如何協助改善 JDBC 驅動程式？**  
JDBC 驅動程式是開放原始碼和原始程式碼位於[GitHub](https://github.com/microsoft/mssql-jdbc)。 您可以協助改善驅動程式所提出的問題，並且積極參與程式碼基底。

**此驅動程式支援哪些版本的 SQL Server 及 Java？**  
 請參閱[Microsoft JDBC Driver for SQL Server 支援對照表](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md)頁面以取得詳細資料。  
  
 **升級我的驅動程式時，我應該知道什麼？**  
 Microsoft JDBC 驅動程式 6.2 支援 JDBC 4.0、 4.1 和 4.2 規格，並安裝封裝中包含兩個 JAR 類別庫時，也將，如下所示：  
  
|JAR|JDBC 規格|JDK 版本|  
|-|-|-|  
|mssql-jdbc-6.2.1.jre8.jar|JDBC 4.2、4.1 及 4.0|JDK 8.0|  
|mssql-jdbc-6.2.1.jre7.jar|JDBC 4.1 及 4.0|JDK 7.0|  
 
 Microsoft JDBC Drivers 6.0 和 4.2 for SQL Server 支援 JDBC 4.0、 4.1 和 4.2 規格，包含兩個 JAR 類別庫中的安裝套件，如下所示：  
  
|JAR|JDBC 規格|JDK 版本|   
|-|-|-|  
|sqljdbc42.jar|JDBC 4.2、4.1 及 4.0|JDK 8.0|  
|sqljdbc41.jar|JDBC 4.1 及 4.0|JDK 7.0|  
  
 Microsoft JDBC Driver 4.1 for SQL Server 支援 JDBC 4.0 規格，並安裝封裝中包含一個 JAR 類別庫時，也將，如下所示：  
  
|JAR|JDBC 規格|JDK 版本|    
|-|-|-|  
|sqljdbc41.jar|JDBC 4.0|JDK 7.0 和 6.0|
  
 Microsoft JDBC Driver for SQL Server 4.0 支援 JDBC 3.0 與 JDBC 4.0 規格，並各在這兩種規格的安裝封裝中包含了下列兩個 JAR 類別庫：sqljdbc.jar 及 sqljdbc4.jar。  
  
|JAR|JDBC 規格|JDK 版本|   
|-|-|-|  
|sqljdbc4.jar|JDBC 4.0|JDK 6.0 及 5.0|  
|sqljdbc.jar|JDBC 3.0|JDK 6.0 及 5.0|  
  
 **是否需要在我的應用程式使用最新的驅動程式搭配我現有的 SQL Server 版本中進行的任何程式碼變更？**  
 我們通常會設計回溯相容功能，因此，當您升級驅動程式時，並不需要變更現有的應用程式。 確認新的驅動程式版本導入了一項重大變更， [JDBC 驅動程式的版本資訊](../../connect/jdbc/release-notes-for-the-jdbc-driver.md)> 一節將提供清楚的詳細資料變更，而且對現有的應用程式的影響。 此外，您也可以檢閱驅動程式隨附的版本資訊，查看該版本中已經修正之錯誤與已知問題的清單。  
  
 **驅動程式的成本多少？**  
 Microsoft JDBC Driver for SQL Server 為免費提供。  
  
 **可以重新發佈的驅動程式嗎？** JDBC 驅動程式 4.1、 4.2、 6.0 與 6.2 是可轉散發套件。 請檢閱授權合約中的 「 可散布程式碼 」 子句。
 
 JDBC Driver 4.0 是可以自由轉散發個別的轉散發授權需要註冊。 若要註冊，或如需詳細資訊，請參閱我們[轉散發 Microsoft JDBC Driver](../../connect/jdbc/redistributing-the-microsoft-jdbc-driver.md)。 
 
   
 **可以使用驅動程式從 Linux 電腦存取 Microsoft SQL Server？** 當然可以。 您可以使用此驅動程式從 Linux、 Unix 及其他非 Windows 平台存取 SQL Server。 請參閱我們[Microsoft JDBC Driver for SQL Server 支援對照表](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md)如需詳細資訊。  
  
 **此驅動程式是否支援安全通訊端層 (SSL) 加密？** 此驅動程式自 1.2 版起，即支援安全通訊端層 (SSL) 加密。 如需詳細資訊，請參閱[使用 SSL 加密](../../connect/jdbc/using-ssl-encryption.md)。  
  
 **Microsoft JDBC 驅動程式支援哪些驗證類型為 SQL Server？**  
 下表列出可用的驗證選項。 請注意，只有 4.0 版以後的驅動程式，才能使用純 Java Kerberos 驗證。  
  
|||  
|-|-|  
|平台|驗證|  
|非 Windows|純 Java Kerberos|  
|非 Windows|SQL Server|  
|視窗|純 Java Kerberos|  
|視窗|SQL Server|  
|視窗|Kerberos 加 NTLM 備份|  
|視窗|NTLM|  
  
**此驅動程式是否支援網際網路通訊協定第 6 版 (IPv6) 位址？**  
 支援。此驅動程式可以使用 IPv6 位址搭配連接屬性集合 serverName 連接字串屬性。 如需詳細資訊，請參閱[建立連接 URL](../../connect/jdbc/building-the-connection-url.md)。  
  
**什麼是自適性緩衝？**  
 自適性緩衝功能自 Microsoft SQL Server 2005 JDBC Driver 1.2 版起引進，其設計可以擷取任何種類的大型數值資料，但不會額外增加伺服器資料指標的負荷。 Microsoft SQL Server JDBC Driver 的自適性緩衝功能提供連接字串屬性 responseBuffering，可以設定為 "adaptive" 或 "full"。 自 JDBC Driver 2.0 版起，此驅動程式的預設行為是 "adaptive"。 換言之，若要取得適應性緩衝行為，您的應用程式不需要明確要求適應性行為。 但在 1.2 版中，預設的緩衝模式為 "full"，且應用程式必須明確要求自適性緩衝的模式。 如需詳細資訊，請參閱[使用適應性緩衝](../../connect/jdbc/using-adaptive-buffering.md)主題和部落格[什麼 adaptiveresponse 緩衝和為什麼應該使用它？](http://go.microsoft.com/fwlink/?LinkId=111575)。  
  
**驅動程式支援連接共用嗎？**  
 此驅動程式提供支援 Java Platform, Enterprise Edition 5 (Java EE 5) 的連接共用。 此驅動程式實作了 JDBC 3.0 所需的介面，讓驅動程式能夠參與中介軟體應用程式廠商所提供的連接共用實作。 此驅動程式可參與這些環境中的共用連接。 如需詳細資訊，請參閱[使用連接共用](../../connect/jdbc/using-connection-pooling.md)。 此驅動程式不提供自己的共用實作，而會使用第三方 Java 應用程式伺服器。  
  
**是可用的驅動程式支援？**  
 此驅動程式提供數個支援選項。 您可以將問題張貼或簽發給我們[GitHub 儲存機制](https://github.com/microsoft/mssql-jdbc)這由 Microsoft 所監視。 [論壇](http://go.microsoft.com/fwlink/?LinkID=246673)受 Microsoft、 MVP 及社群。 您也可以連絡 Microsoft 客戶支援服務。 我們可能會要求您重現任何第三方應用程式伺服器以外的問題。 若無法在裝載 Java 容器之環境以外之處重現問題，您必須連絡相關的第三方廠商，我們才能繼續協助您。 我們也可能要求您在作業系統 (例如 Windows) 上重現您的問題，以便能提出最適合您的協助。  
  
**適用於任何第三方應用程式伺服器認證的驅動程式嗎？**
此驅動程式已在多種應用程式伺服器上進行過測試，包括 IBM WebSphere 及 SAP NetWeaver。  
  
**如何啟用追蹤？**  
 此驅動程式支援追蹤 (或記錄) 功能，可用於協助解決在應用程式中使用 JDBC 驅動程式時所發生的問題。 為能在用戶端上使用 JAR 追蹤，JDBC 驅動程式會使用 java.util.logging 中的記錄 API java.util.logging。 如需詳細資訊，請參閱[追蹤驅動程式作業](../../connect/jdbc/tracing-driver-operation.md)。 對於伺服器端的 XA 追蹤，請參閱 [Data Access Tracing in SQL Server](http://go.microsoft.com/fwlink/?LinkId=248705)(SQL Server 的資料存取追蹤)。  
  
**哪裡可以下載舊版的 SQL Server 2000 的 JDBC 驅動程式，2005年驅動程式，例如驅動程式 1.0、 1.1 或 1.2 驅動程式？**  
 因為已經停止支援這些驅動程式版本，所以也不再提供其下載。 因為我們會持續改進 Java 連接性支援， 所以極力建議您使用最新版的 JDBC 驅動程式。  
  
 **我使用 JRE 1.4。哪一個驅動程式是與 JRE 1.4 相容**對於使用 SAP 產品並需要 JRE 1.4 支援的客戶，您可以連絡[SAPService Marketplace](http://service.sap.com/)取得 1.2 Microsoft JDBC 驅動程式。  
  
**可以使用 FIPS 驗證演算法通訊驅動程式嗎？** Microsoft JDBC Driver 不含任何密碼編譯演算法。 若客戶使用作業系統、應用程式及聯邦資訊處理標準 (FIPS) 可接受的 JVM 演算法，並將驅動程式設定成使用這些演算法，則此驅動程式將只會使用指定的演算法進行通訊。  
  
  

