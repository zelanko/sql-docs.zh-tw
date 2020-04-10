---
title: 連線到 SQL Server │ Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data source names
- connection string keywords
- DSNs
ms.assetid: f95cdbce-e7c2-4e56-a9f7-8fa3a920a125
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d323481aaf3e12da9786a3b02f21f47c3c98f7cf
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924535"
---
# <a name="connecting-to-sql-server"></a>連線到 SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本主題討論如何建立與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫之間的連線。  
  
## <a name="connection-properties"></a>Connection Properties  

如需 Linux 和 Mac 上支援的所有連接字串關鍵字和屬性，請參閱 [DSN 和連接字串關鍵字和屬性](../../../connect/odbc/dsn-connection-string-attribute.md)

> [!IMPORTANT]  
> 連接到使用資料庫鏡像的資料庫 (具有容錯移轉夥伴) 時，請不要在連接字串中指定資料庫名稱。 但是，請傳送 **use** _database_name_ 命令，以便在執行查詢前先連線到資料庫。  
  
傳遞至**驅動程式**關鍵字的值可以是下列其中之一：  
  
-   安裝驅動程式時所使用的名稱。

-   驅動程式庫的路徑，指定於用來安裝驅動程序的範本 .ini 檔案中。  

若要建立 DSN，請建立 (如有必要) 並編輯檔案 **~/.odbc.ini** (主目錄中的 `.odbc.ini`)，以取得僅供目前使用者存取的使用者 DSN，或編輯 `/etc/odbc.ini` 以取得系統 DSN (需要系統管理權限)。以下是範例檔案，其中顯示 DSN 的最低必要項目：  

```  
[MSSQLTest]  
Driver = ODBC Driver 13 for SQL Server  
Server = [protocol:]server[,port]  
#   
# Note:  
# Port is not a valid keyword in the odbc.ini file  
# for the Microsoft ODBC driver on Linux or macOS
#  
```  

您可以選擇性地指定用以連接到伺服器的通訊協定和連接埠。 例如，**Server=tcp:** _servername_ **,12345**。 請注意，Linux 和 macOS 驅動程式所支援的唯一通訊協定是 `tcp`。

若要在靜態連接埠上連線到具名執行個體，請使用 <b>Server=</b>伺服器名稱  ,**port_number**。 在 17.4 版之前，不支援連線到動態連接埠。

或者，您可將 DSN 資訊新增至範本檔案，並執行下列命令將其新增至 `~/.odbc.ini`：
 - **odbcinst -i -s -f** _template_file_  
 
您可以使用 `isql` 測試連接，以確認您的驅動程式可運作，或者您可以使用下列命令：
 - **bcp master.INFORMATION_SCHEMA.TABLES out OutFile.dat -S <server> -U <name> -P <password>**  

## <a name="using-secure-sockets-layer-ssl"></a>使用安全通訊端層 (SSL)  
您可以使用安全通訊端層 (SSL) 加密與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的連線。 SSL 會保護網路上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用者名稱和密碼。 SSL 也會驗證伺服器的身分識別，以防止攔截式 (MITM) 攻擊。  

啟用加密可提高安全性，但會犧牲效能。

如需詳細資訊，請參閱[加密 SQL Server 的連接](https://go.microsoft.com/fwlink/?LinkId=220900)和[使用加密而不需驗證](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)。

無論 **Encrypt** 和 **TrustServerCertificate**的設定為何，伺服器登入認證 (使用者名稱和密碼) 一律都會加密。 下表說明 **Encrypt** 和 **TrustServerCertificate** 設定的效用。  

||**TrustServerCertificate=no**|**TrustServerCertificate=yes**|  
|-|-------------------------------------|------------------------------------|  
|**Encrypt=no**|不檢查伺服器憑證。<br /><br />在用戶端和伺服器之間傳送的資料不會加密。|不檢查伺服器憑證。<br /><br />在用戶端和伺服器之間傳送的資料不會加密。|  
|**Encrypt=yes**|會檢查伺服器憑證。<br /><br />在用戶端和伺服器之間傳送的資料會加密。<br /><br />[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SSL 憑證內主體一般名稱 (CN) 或主體別名 (SAN) 中的名稱 (或 IP 位址) 應完全符合指定在連接字串中的伺服器名稱 (或 IP 位址)。|不檢查伺服器憑證。<br /><br />在用戶端和伺服器之間傳送的資料會加密。|  

根據預設，加密的連線一律會驗證伺服器的憑證。 不過，如果您連接到具有自我簽署憑證的伺服器，也請新增 `TrustServerCertificate` 選項，以略過檢查憑證是否符合受信任憑證授權單位的清單：  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
SSL 會使用 OpenSSL 程式庫。 下表顯示 OpenSSL 的最低支援版本，以及每個平台的預設憑證信任存放區位置：

|平台|最低 OpenSSL 版本|預設憑證信任存放區位置|  
|------------|---------------------------|--------------------------------------------|
|Debian 10|1.1.1|/etc/ssl/certs|
|Debian 9|1.1.0|/etc/ssl/certs|
|Debian 8.71|1.0.1|/etc/ssl/certs|
|OS X 10.11、macOS 10.12、10.13、10.14|1.0.2|/usr/local/etc/openssl/certs|
|Red Hat Enterprise Linux 8|1.1.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 7|1.0.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|
|SUSE Linux Enterprise 15|1.1.0|/etc/ssl/certs|
|SUSE Linux Enterprise 11、12|1.0.1|/etc/ssl/certs|
|Ubuntu 18.10、19.04|1.1.1|/etc/ssl/certs|
|Ubuntu 18.04|1.1.0|/etc/ssl/certs|
|Ubuntu 16.04、16.10、17.10|1.0.2|/etc/ssl/certs|
|Ubuntu 14.04|1.0.1|/etc/ssl/certs|

當您使用 **SQLDriverConnect** 連接時，也可以使用 `Encrypt` 選項指定連接字串中的加密。

## <a name="adjusting-the-tcp-keep-alive-settings"></a>調整 TCP Keep-Alive 設定

從 ODBC 驅動程式 17.4 開始，可設定驅動程式傳送 keep-alive 封包，並在未收到回應時重新傳輸這些封包的頻率。
若要設定，請將下列設定新增至 `odbcinst.ini` 中的驅動程式區段，或 `odbc.ini` 中的 DSN 區段。 使用 DSN 連線時，驅動程式將會使用 DSN 區段中的設定 (如果有的話)；如果只使用連接字串連接，則會使用 `odbcinst.ini` 中驅動程式區段內的設定。 如果此這設定不存在任一個位置中，驅動程式會使用預設值。

- `KeepAlive=<integer>` 會藉由傳送 keep-alive 封包，控制 TCP 嘗試驗證閒置連線是否仍完整無缺的頻率。 預設值是 **30** 秒。

- `KeepAliveInterval=<integer>` 可決定在收到回應之前，用以分隔 keep-alive 重新傳輸的間隔。  預設值為 **1** 秒。

## <a name="see-also"></a>另請參閱

- [在 Linux 上安裝 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [在 macOS 上安裝 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md)
- [程式設計指導方針](../../../connect/odbc/linux-mac/programming-guidelines.md)
