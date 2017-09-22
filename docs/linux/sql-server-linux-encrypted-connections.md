---
title: "加密 SQL Server on Linux 連接 |Microsoft 文件"
description: "本主題說明在 Linux 上的加密連接到 SQL Server。"
author: tmullaney
ms.date: 06/14/2017
ms.author: thmullan;rickbyh
manager: jhubbard
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
helpviewer_keywords:
- Linux, encrypted connections
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 47a15701730019aaf166743c47c606aa2059b7fe
ms.contentlocale: zh-tw
ms.lasthandoff: 08/28/2017

---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>加密連接到 SQL Server on Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Linux 上可以使用傳輸層安全性 (TLS) 來加密資料的用戶端應用程式和執行個體之間透過網路傳送[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Windows 和 Linux 上支援相同的 TLS 通訊協定： TLS 1.2、 1.1 和 1.0。 不過，設定 TLS 的步驟會在其上的作業系統特定的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]正在執行。  
 
## <a name="typical-scenario"></a>典型案例 
TLS 用來加密從用戶端應用程式的連線[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 如果設定正確，TLS 提供隱私權與資料完整性，以用戶端與伺服器之間的通訊。  
下列步驟說明典型的案例：  

1. 資料庫管理員會產生私用金鑰和憑證簽署要求 (CSR)。 CSR 的一般名稱必須符合用戶端在其 SQL Server 連接字串中指定的伺服器名稱。 此一般名稱通常是完整的網域名稱[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主機。 若要使用多部伺服器相同的憑證，您可以使用萬用字元的一般名稱 (例如，`"*.contoso.com"`而不是`"node1.contoso.com"`)。   
2. CSR 會傳送至憑證授權單位 (CA) 簽署。 應該用來連接的所有用戶端電腦信任的 CA [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 CA 會傳回的簽署的憑證的資料庫管理員。   
3. 資料庫系統管理員設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]TLS 連線使用的私用金鑰和簽署的憑證。   
4. 用戶端指定`"Encrypt=True"`和`"TrustServerCertificate=False"`在其連接字串中。 （特定的參數名稱，可能正在使用哪一個驅動程式而有所不同）。 用戶端現在嘗試連接到 SQL Server 加密，並檢查 SQL Server 憑證，以防止攔截攻擊的有效性。  
 
## <a name="configuring-tls-on-linux"></a>設定 Linux 上的 TLS  

使用`mssql-conf`執行個體設定 TLS[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Linux 上執行。 支援下列選項：  

|選項 |Description |
|--- |--- |
|`network.forceencryption` |如果是 1，然後[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]會強制所有連線必須加密。 根據預設，此選項為 0。 |  
|`network.tlscert` |憑證的絕對路徑檔[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]用於 TLS。 範例：`/etc/ssl/certs/mssql.pem`憑證檔案必須是可由 mssql 帳戶存取。 Microsoft 建議限制對檔案使用存取`chown mssql:mssql <file>; chmod 400 <file>`。 |  
|`network.tlskey` |私用金鑰的絕對路徑檔[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]用於 TLS。 範例：`/etc/ssl/private/mssql.key`憑證檔案必須是可由 mssql 帳戶存取。 Microsoft 建議限制對檔案使用存取`chown mssql:mssql <file>; chmod 400 <file>`。 | 
|`network.tlsprotocols` |以逗號分隔清單的哪一個 TLS 通訊協定所允許 SQL Server。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]一律會嘗試交涉的最強的允許通訊協定。 如果用戶端不支援任何允許的通訊協定，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]會拒絕連線嘗試。  為了相容性，允許進行所有支援的通訊協定的預設 （1.2、 1.1、 1.0）。  如果您的用戶端支援 TLS 1.2，Microsoft 建議允許只 TLS 1.2。 |  
|`network.tlsciphers` |指定所允許的密碼[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]tls。 這個字串必須格式化每個[OpenSSL 的加密清單格式](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html)。 一般情況下，您應該不需要變更這個選項。 <br /> 根據預設，可使用下列密碼： <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |   
| | |
 
## <a name="example"></a>範例 
這個範例會使用自我簽署的憑證。 在一般實際執行案例中，會由所有用戶端信任的 CA 所簽署憑證。  
 
### <a name="step-1-generate-private-key-and-certificate"></a>步驟 1： 產生私用金鑰和憑證 
開啟 終端機 Linux 機器上的命令位置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]正在執行。 執行下列命令：  

- 產生自我簽署的憑證。 請確定 /CN 符合您的 SQL Server 主機完整網域名稱。 您可能選擇性地使用萬用字元，例如`'/CN=*.contoso.com'`。    
   ```  
   openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
   ```  

- 限制存取權`mssql`  
   ```  
   sudo chown mssql:mssql mssql.pem mssql.key 
   sudo chmod 600 mssql.pem mssql.key 
   ```  
 
- 移至系統 SSL 目錄 （選擇性）  
   ```  
   sudo mv mssql.pem /etc/ssl/certs/ 
   sudo mv mssql.key /etc/ssl/private/ 
   ```  
 
### <a name="step-2-configure--includessnoversionincludesssnoversion-mdmd"></a>步驟 2： 設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
使用`mssql-conf`設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用憑證和金鑰 TLS。 為了提高安全性，您也可以 TLS 1.2 設定為只允許通訊協定，並強制使用加密的連接的所有用戶端。  

```  
sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pem 
sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.key 
sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
sudo /opt/mssql/bin/mssql-conf set network.forceencryption 1 
```
 
### <a name="step-3-restart-includessnoversionincludesssnoversion-mdmd"></a>步驟 3： 重新啟動[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]必須重新啟動這些變更才會生效。  
`sudo systemctl restart mssql-server`  
 
### <a name="step-4-copy-self-signed-certificate-to-client-machines"></a>步驟 4： 將複製到用戶端電腦的自我簽署的憑證 
由於這個範例會使用自我簽署的憑證[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主機，必須複製及安裝為連接到的所有用戶端電腦上受信任的根憑證的憑證 （不是私密金鑰） [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 如果憑證由所有用戶端已經信任的 CA 所簽署，不需要此步驟。 
 
### <a name="step-5-connect-from-clients-using-tls"></a>從 使用 TLS 用戶端連接的步驟 5: 
連接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]從啟用加密的用戶端和`TrustServerCertificate`設`False`連接字串中。 以下是如何指定這些參數使用不同的工具和驅動程式的一些範例。 

sqlcmd  
`sqlcmd -N -C -S mssql.contoso.com -U sa -P '<YourPassword>'`  

[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]   
  ![SSMS 連接對話方塊](media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "SSMS 連接對話方塊")  
  
ADO.NET  
`"Encrypt=true; TrustServerCertificate=true;"`  

ODBC   
`"Encrypt=yes; TrustServerCertificate=no;"`  

JDBC  
`"encrypt=true; trustServerCertificate=false;" `

 
## <a name="common-connection-errors"></a>一般連接錯誤  

|錯誤訊息 |Fix |
|--- |--- |
|不受信任授權單位所核發的憑證鏈結。  |當用戶端無法驗證 SQL Server 的 TLS 信號交換期間出示的憑證上的簽章時，就會發生此錯誤。 請確定用戶端所信任是[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]直接，憑證或 CA 簽署的 SQL Server 憑證。 |
|目標主體名稱不正確。  |請確定 SQL 伺服器的憑證上的 [一般名稱] 欄位符合用戶端的連接字串中指定的伺服器名稱。 |  
|遠端主機已強制關閉現有的連接。 |當用戶端不支援所需的 SQL Server 的 TLS 通訊協定版本，就會發生此錯誤。 例如，如果[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]已設定為需要 TLS 1.2，請確定您的用戶端也支援 TLS 1.2 通訊協定。 |
| | |   


