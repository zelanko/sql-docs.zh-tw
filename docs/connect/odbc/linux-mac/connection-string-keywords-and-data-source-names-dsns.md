---
title: 連接到 SQL Server |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data source names
- connection string keywords
- DSNs
ms.assetid: f95cdbce-e7c2-4e56-a9f7-8fa3a920a125
caps.latest.revision: 41
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f49c0105f96f446c627f5ec1b5f47ee62b28558
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-sql-server"></a>連線到 SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本主題討論如何建立的連接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料庫。  
  
## <a name="connection-properties"></a>連接屬性  

請參閱[DSN 和連接字串關鍵字和屬性](../../../connect/odbc/dsn-connection-string-attribute.md)所有的連接字串關鍵字與支援 Linux 和 Mac 上的屬性

> [!IMPORTANT]  
> 連接到使用資料庫鏡像的資料庫 (具有容錯移轉夥伴) 時，請不要在連接字串中指定資料庫名稱。 相反地，傳送**使用** *database_name*命令來執行查詢之前，連接到資料庫。  
  
傳遞給的值**驅動程式**關鍵字可以是下列其中之一：  
  
-   安裝驅動程式時所使用的名稱。

-   要用來安裝驅動程式的範本.ini 檔案中指定的驅動程式程式庫的路徑。  

若要建立 DSN，建立 （如有必要），並編輯檔案 **~/.odbc.ini** (`.odbc.ini`主目錄中) 與目前的使用者只能存取使用者 dsn 或`/etc/odbc.ini`系統 dsn （需要管理權限。）以下是範例檔案，其中顯示 dsn 的最少的必要項目：  

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

您可以選擇性地指定用以連接到伺服器的通訊協定和連接埠。 例如， **Server = tcp:***servername***、 12345**。 請注意，唯一支援的 Linux 及 macOS 驅動程式的通訊協定是`tcp`。

若要連接到具名執行個體上的靜態連接埠，使用<b>Server =</b>*servername*，**port_number**。 不支援連接到動態連接埠。  

或者，您可以將 DSN 資訊加入至範本檔案，並執行下列命令，以便將它加入至`~/.odbc.ini`:
 - **odbcinst-i-f-s** *template_file*  
 
您可以確認您的驅動程式正在使用`isql`來測試連接，或者您可以使用此命令：
 - **bcp master.INFORMATION_SCHEMA.TABLES 出 OutFile.dat-S <server> -U <name> -P <password>**  

## <a name="using-secure-sockets-layer-ssl"></a>使用安全通訊端層 (SSL)  
您可以使用安全通訊端層 (SSL) 加密連線[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。 SSL 會保護[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]使用者名稱和透過網路的密碼。 SSL 也會驗證伺服器的身分識別，以防止攔截式 (MITM) 攻擊。  

啟用加密可提高安全性，但會犧牲效能。

如需詳細資訊，請參閱[加密對 SQL Server 的連線](http://go.microsoft.com/fwlink/?LinkId=220900)和[使用加密而不需驗證](https://docs.microsoft.com/en-us/sql/relational-databases/native-client/features/using-encryption-without-validation)。

無論 **Encrypt** 和 **TrustServerCertificate**的設定為何，伺服器登入認證 (使用者名稱和密碼) 一律都會加密。 下表說明 **Encrypt** 和 **TrustServerCertificate** 設定的效用。  

||**TrustServerCertificate=no**|**TrustServerCertificate=yes**|  
|-|-------------------------------------|------------------------------------|  
|**Encrypt=no**|不檢查伺服器憑證。<br /><br />在用戶端和伺服器之間傳送的資料不會加密。|不檢查伺服器憑證。<br /><br />在用戶端和伺服器之間傳送的資料不會加密。|  
|**Encrypt=yes**|會檢查伺服器憑證。<br /><br />在用戶端和伺服器之間傳送的資料會加密。<br /><br />在主體一般名稱 (CN) 或主體別名 (SAN) 中的名稱 （或 IP 位址） [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL 憑證應完全符合的伺服器名稱 （或 IP 位址） 連接字串中指定。|不檢查伺服器憑證。<br /><br />在用戶端和伺服器之間傳送的資料會加密。|  

根據預設，加密的連接一律會驗證伺服器的憑證。 不過，如果您連接到已自我簽署的憑證的伺服器，也將`TrustServerCertificate`略過檢查憑證的受信任的憑證授權單位清單進行比對的選項：  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
SSL 會使用 OpenSSL 程式庫。 下表顯示 OpenSSL 的最低支援版本，以及每個平台的預設憑證信任存放區位置：

|平台|最低 OpenSSL 版本|預設憑證信任存放區位置|  
|------------|---------------------------|--------------------------------------------|
|Debian 9|1.1.0|/etc/ssl/certs|
|Debian 8.71 |1.0.1|/etc/ssl/certs|
|macOS 10.13|1.0.2|/usr/local/etc/openssl/certs|
|macOS 10.12|1.0.2|/usr/local/etc/openssl/certs|
|OS X 10.11|1.0.2|/usr/local/etc/openssl/certs|
|Red Hat Enterprise Linux 7|1.0.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|
|SuSE Linux Enterprise 12 |1.0.1|/etc/ssl/certs|
|SuSE Linux Enterprise 11 |0.9.8|/etc/ssl/certs|
|Ubuntu 17.10 |1.0.2|/etc/ssl/certs|
|Ubuntu 16.10 |1.0.2|/etc/ssl/certs|
|Ubuntu 16.04 |1.0.2|/etc/ssl/certs|
  
您也可以指定加密連接字串使用`Encrypt`選項使用時**SQLDriverConnect**連接。

## <a name="see-also"></a>另請參閱  
[安裝的 Microsoft ODBC Driver for SQL Server on Linux 及 macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)  
[程式設計指導方針](../../../connect/odbc/linux-mac/programming-guidelines.md)
