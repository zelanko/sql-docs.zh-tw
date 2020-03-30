---
title: Linux 和 macOS 上的 ODBC 驅動程式 - 高可用性和災害復原 | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fa656c5b-a935-40bf-bc20-e517ca5cd0ba
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 08fb8cc6e54fff4b315a0a98ace046a49b2673a3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "68008776"
---
# <a name="odbc-driver-on-linux-and-macos-support-for-high-availability-and-disaster-recovery"></a>Linux 和 macOS 上的 ODBC 驅動程式 - 高可用性和災害復原的支援
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Linux 和 macOS 的 ODBC 驅動程式支援 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]。 如需 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]的相關資訊，請參閱：  
  
-   [可用性群組接聽程式、用戶端連線及應用程式容錯移轉 (SQL Server)](https://msdn.microsoft.com/library/hh213417.aspx)  
  
-   [建立及設定可用性群組 (SQL Server)](https://msdn.microsoft.com/library/ff878265.aspx)  
  
-   [容錯移轉叢集和 AlwaysOn 可用性群組 (SQL Server)](https://msdn.microsoft.com/library/ff929171.aspx)  
  
-   [使用中次要：可讀取的次要複本 (AlwaysOn 可用性群組)](https://msdn.microsoft.com/library/ff878253.aspx)  
  
您可以在連接字串中指定給定可用性群組的可用性群組接聽程式。 如果在 Linux 或 macOS 上，ODBC 應用程式連線到可用性群組中發生容錯移轉的資料庫，則原始連線會中斷，而且應用程式必須在容錯移轉後開啟新連線，才能繼續工作。

如果您未連線到可用性群組接聽程式，而且多個 IP 位址與主機名稱建立關聯，則 Linux 和 macOS 上的 ODBC 驅動程式會循序逐一查看與 DNS 主機名稱建立關聯的所有 IP 位址。

如果無法連線到 DNS 伺服器第一個傳回的 IP 位址，這些反覆運算可能會很費時。 在連線到可用性群組接聽程式時，驅動程式會嘗試平行建立對所有 IP 位址的連線。 如果連接嘗試成功，驅動程式就會捨棄任何暫止的連接嘗試。

> [!NOTE]  
> 連線可能會由於可用性群組容錯移轉而失敗，因此請實作連線重試邏輯，並重試失敗的連線，直到重新連線為止。 增加連接逾時並實作連接重試邏輯，可提高連接到可用性群組的機率。

## <a name="connecting-with-multisubnetfailover"></a>使用 MultiSubnetFailover 進行連接

在連線到**可用性群組接聽程式或**容錯移轉叢集執行個體時，請一律指定 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]MultiSubnetFailover=Yes[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]。 **MultiSubnetFailover** 可讓 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中的所有可用性群組和容錯移轉叢集執行個體更快速地容錯移轉。 **MultiSubnetFailover** 也會大幅縮短單一和多重子網路 AlwaysOn 拓撲的容錯移轉時間。 在多重子網路容錯移轉期間，用戶端會嘗試平行連接。 在子網路容錯移轉期間，驅動程式會積極重試 TCP 連接。

**MultiSubnetFailover** 連接屬性表示應用程式正在可用性群組或容錯移轉叢集執行個體中部署。 驅動程式會嘗試連線到所有 IP 位址，以嘗試連線到主要 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上的資料庫。 透過 **MultiSubnetFailover=Yes** 進行連線時，用戶端重試 TCP 連線之速度會比作業系統的預設 TCP 重新傳輸間隔快。 **MultiSubnetFailover=Yes** 可在容錯移轉 AlwaysOn 可用性群組或 AlwaysOn 容錯移轉叢集執行個體之後更快速地重新連接。 **MultiSubnetFailover=Yes** 適用於單一和多重子網路可用性群組與容錯移轉叢集執行個體。  

在連接到可用性群組接聽程式或容錯移轉叢集執行個體時，請使用 **MultiSubnetFailover=Yes** 。 否則，您的應用程式效能可能會受到負面影響。

連線到可用性群組或容錯移轉叢集執行個體中的伺服器時，請注意下列：
  
-   連線到單一子網路或多重子網路可用性群組時，指定 **MultiSubnetFailover=Yes** 提高效能。

-   在連接字串中指定可用性群組的可用性群組接聽程式作為伺服器。
  
-   您無法連線到設定了超過 64 個 IP 位址的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體。

-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證或 Kerberos 驗證都可以搭配 **MultiSubnetFailover=Yes** 使用，而不會影響應用程式的行為。

-   您可以增加 **loginTimeout** 的值，以容納容錯移轉時間並減少應用程式連接重試次數。

-   不支援分散式工作階段。  
  
如果唯讀路由不在作用中，在下列狀況下，連接到可用性群組中的次要複本位置將會失敗：  
  
1.  如果未設定次要複本位置接受連接。  
  
2.  如果應用程式使用 **ApplicationIntent=ReadWrite** ，而且已針對唯讀存取設定次要複本位置。  
  
如果設定主要複本拒絕唯讀工作負載，而且連接字串包含 **ApplicationIntent=ReadOnly**，則連接會失敗。  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="odbc-syntax"></a>ODBC 語法

有兩個 ODBC 連接字串關鍵字支援 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]：  
  
-   **ApplicationIntent**  
  
-   **MultiSubnetFailover**  
  
如需 ODBC 連接字串關鍵字的詳細資訊，請參閱[搭配 SQL Server Native Client 使用連接字串關鍵字](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
同等的連接屬性如下：
  
-   **SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
如需 ODBC 連線屬性的詳細資訊，請參閱 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)。  
  
使用 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)] 的 ODBC 應用程式可使用兩個函式的其中一個來進行連線：  
  
|函式|描述|  
|------------|---------------|  
|[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)|**SQLConnect** 可透過資料來源名稱 (DSN) 或連線屬性來支援 **ApplicationIntent** 和 **MultiSubnetFailover**。|  
|[SQLDriverConnect 函式](../../../odbc/reference/syntax/sqldriverconnect-function.md)|**SQLDriverConnect** 可透過 DSN、連接字串或連線屬性來支援 **ApplicationIntent** 和 **MultiSubnetFailover**。|
  
## <a name="see-also"></a>另請參閱  

[連接字串關鍵字和資料來源名稱 (DSN)](../../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)

[程式設計指導方針](../../../connect/odbc/linux-mac/programming-guidelines.md)

[版本資訊](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  
