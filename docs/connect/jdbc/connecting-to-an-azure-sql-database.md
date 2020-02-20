---
title: 連線到 Azure SQL 資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 49645b1f-39b1-4757-bda1-c51ebc375c34
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 58a0b6f11fa28dca0e8aae98cb1794b12e3fc227
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "70155104"
---
# <a name="connecting-to-an-azure-sql-database"></a>連接到 Azure SQL Database

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文討論使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 來連線到 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 時發生的問題。 如需連線到 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 的詳細資訊，請參閱：  
  
- [SQL Azure 資料庫](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)  
  
- [操作說明：使用 JDBC 連線到 SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)  

- [使用 Azure Active Directory 驗證連接](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)  
  
## <a name="details"></a>詳細資料

連線到 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 時，您應該連線到 master 資料庫來呼叫 **SQLServerDatabaseMetaData.getCatalogs**。  
[!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 不支援從使用者資料庫傳回整組目錄。 **SQLServerDatabaseMetaData.getCatalogs** 會使用 sys.databases 檢視來取得目錄。 請參閱 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 中對於權限的討論，以了解 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 上的 **SQLServerDatabaseMetaData.getCatalogs** 行為。  
  
## <a name="connections-dropped"></a>連線中斷

連線到 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 時，網路元件 (例如防火牆) 可能會在一段時間沒有活動之後結束閒置連線。 在此內容中，有兩種閒置連接類型：  

- TCP 層閒置，其中任何數目的網路裝置都可能會卸除連接。  

- SQL Azure 閘道閒置，其中可能會發生 TCP **keepalive** 訊息 (使連線從 TCP 觀點而言未閒置)，但在 30 分鐘內沒有使用中查詢。 在此狀況下，閘道會在 30 分鐘時判定 TDS 連接閒置並結束連接。  
  
若要避免網路元件中斷閒置連接，您應該在載入此驅動程式的作業系統上設定下列登錄設定 (或其非 Windows 對等項目)：  
  
|登錄設定|建議值|  
|----------------------|-----------------------|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ Parameters \ KeepAliveTime|30000|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ Parameters \ KeepAliveInterval|1000|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ Parameters \ TcpMaxDataRetransmissions|10|  
  
重新啟動電腦，讓這些登錄設定生效。  

若要在 Azure 中執行時完成此作業，請建立啟動工作以加入登錄機碼。  例如，您可以將下列啟動工作加入至服務定義檔：  

```xml
<Startup>  
    <Task commandLine="AddKeepAlive.cmd" executionContext="elevated" taskType="simple">  
    </Task>  
</Startup>  
```

然後，將 AddKeepAlive.cmd 檔案加入至您的專案。 將 [複製到輸出目錄] 設定設為 [永遠複製]。 下面是範例 AddKeepAlive.cmd 檔案：  

```bat
if exist keepalive.txt goto done  
time /t > keepalive.txt  
REM Workaround for JDBC keep alive on SQL Azure  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveTime /t REG_DWORD /d 30000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveInterval /t REG_DWORD /d 1000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v TcpMaxDataRetransmissions /t REG_DWORD /d 10 >> keepalive.txt  
shutdown /r /t 1  
:done  
```

## <a name="appending-the-server-name-to-the-userid-in-the-connection-string"></a>將伺服器名稱附加至連接字串中的 userId  

在 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 4.0 版之前，連線到 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 時，您必須將伺服器名稱附加至連接字串中的 UserId。 例如： user@servername 。 從 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 4.0 版開始，您不再需要將 @servername 附加至連接字串中的 UserId。  

## <a name="using-encryption-requires-setting-hostnameincertificate"></a>使用加密需要設定 hostNameInCertificate

在 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 7.2 版之前，連線到 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 時，如果您指定了 **encrypt=true** (如果連接字串中的伺服器名稱為 *shortName*.*domainName*，請將 **hostNameInCertificate** 屬性設定為 \*.*domainName*)，則應該指定 **hostNameInCertificate**。 從驅動程式 7.2 版開始，這個屬性是選擇性的。

例如：

```java
jdbc:sqlserver://abcd.int.mscds.com;databaseName=myDatabase;user=myName;password=myPassword;encrypt=true;hostNameInCertificate=*.int.mscds.com;
```

## <a name="see-also"></a>另請參閱

[使用 JDBC 驅動程式連線到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
