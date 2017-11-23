---
title: "連接到 Azure SQL database |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 49645b1f-39b1-4757-bda1-c51ebc375c34
caps.latest.revision: "23"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: bc0a49d5758b4e7160ecf5e9e374d4c460755161
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="connecting-to-an-azure-sql-database"></a>連接到 Azure SQL Database
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  本主題討論的問題，當使用[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]連接到[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]。 如需有關連接到[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]，請參閱：  
  
-   [SQL Azure 資料庫](http://go.microsoft.com/fwlink/?LinkID=202490)  
  
-   [如何： 連接到使用 JDBC 的 SQL Azure](http://msdn.microsoft.com/library/gg715284.aspx)  
  
-   [使用 java 的 SQL Azure](http://msdn.microsoft.com/library/windowsazure/hh749029(VS.103).aspx)

-   [使用 Azure Active Directory 驗證連接](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)  
  
## <a name="details"></a>詳細資料  
 當連接到[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]，您應該連接至 master 資料庫，才能呼叫**SQLServerDatabaseMetaData.getCatalogs**。  
 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]不支援從使用者資料庫傳回整組目錄。 **SQLServerDatabaseMetaData.getCatalogs**使用 sys.databases 檢視取得目錄。 中的權限討論內容，請參閱[sys.databases （SQL Azure 資料庫）](http://go.microsoft.com/fwlink/?LinkId=217396)來了解**SQLServerDatabaseMetaData.getCatalogs**行為[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]。  
  
 連接中斷  
 當連接到[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]，在一段時間後網路元件 （例如防火牆） 可能會終止閒置連接。 在此內容中，有兩種閒置連接類型：  
  
-   TCP 層閒置，其中任何數目的網路裝置都可能會卸除連接。  
  
-   SQL Azure 閘道閒置，其中 TCP **keepalive**訊息可能會發生 （使連接從 TCP 觀點而言未閒置），但在 30 分鐘內沒有使用中查詢。 在此狀況下，閘道會在 30 分鐘時判定 TDS 連接閒置並結束連接。  
  
 若要避免網路元件中斷閒置連接，您應該在載入此驅動程式的作業系統上設定下列登錄設定 (或其非 Windows 對等項目)：  
  
|登錄設定|建議值|  
|----------------------|-----------------------|  
|HKEY_LOCAL_MACHINE \ 系統 \ CurrentControlSet \ 服務 \ Tcpip \ 參數 \ KeepAliveTime|30000|  
|HKEY_LOCAL_MACHINE \ 系統 \ CurrentControlSet \ 服務 \ Tcpip \ 參數 \ KeepAliveInterval|1000|  
|HKEY_LOCAL_MACHINE \ 系統 \ CurrentControlSet \ 服務 \ Tcpip \ 參數 \ TcpMaxDataRetransmissions|10|  
  
 然後，您必須重新啟動電腦，才能讓這些登錄設定生效。  
  
 若要在 Windows Azure 中執行時完成此作業，請建立啟動工作以加入登錄機碼。  例如，您可以將下列啟動工作加入至服務定義檔：  
  
```  
<Startup>  
    <Task commandLine="AddKeepAlive.cmd" executionContext="elevated" taskType="simple">  
    </Task>  
</Startup>  
```  
  
 然後，將 AddKeepAlive.cmd 檔案加入至您的專案。 將 [複製到輸出目錄] 設定設為 [永遠複製]。 下面是範例 AddKeepAlive.cmd 檔案：  
  
```  
if exist keepalive.txt goto done  
time /t > keepalive.txt  
REM Workaround for JDBC keep alive on SQL Azure  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveTime /t REG_DWORD /d 30000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveInterval /t REG_DWORD /d 1000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v TcpMaxDataRetransmissions /t REG_DWORD /d 10 >> keepalive.txt  
shutdown /r /t 1  
:done  
```  
  
 將伺服器名稱附加至連接字串中的 UserId  
 4.0 版之前[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，當連接到[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]，您必須先將伺服器名稱附加至連接字串中的 UserId。 例如， user@servername。 在 4.0 版開始[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，不再需要附加@servername至連接字串中的 UserId。  
  
 使用加密需要設定 hostNameInCertificate  
 當連接到[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]，您應該指定**hostNameInCertificate**如果您指定**加密 = true**。 (如果連接字串中的伺服器名稱是*shortName*。*domainName*，將**hostNameInCertificate**屬性\*。*domainName*。)  
  
 例如：  
  
```  
jdbc:sqlserver://abcd.int.mscds.com;databaseName= myDatabase;user=myName;password=myPassword;encrypt=true;hostNameInCertificate= *.int.mscds.com;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [使用 JDBC Driver 連接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
