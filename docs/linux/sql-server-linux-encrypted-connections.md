---
title: "加密 SQL Server on Linux 連接 |Microsoft 文件"
description: "本主題說明在 Linux 上的加密連接到 SQL Server。"
author: tmullaney
ms.date: 10/02/2017
ms.author: meetb;rickbyh
manager: jhubbard
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
helpviewer_keywords:
- Linux, encrypted connections
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 41c2caf816ca412e4a6048713dc66f97da5155ae
ms.openlocfilehash: d6beb6350c0d48d35cb3153c2df8eebaec0e4f34
ms.contentlocale: zh-tw
ms.lasthandoff: 10/07/2017

---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>加密連接到 SQL Server on Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Linux 上可以使用傳輸層安全性 (TLS) 來加密資料的用戶端應用程式和執行個體之間透過網路傳送[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Windows 和 Linux 上支援相同的 TLS 通訊協定： TLS 1.2、 1.1 和 1.0。 不過，設定 TLS 的步驟會在其上的作業系統特定的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]正在執行。  

## <a name="requirements-for-certificates"></a>憑證需求 
我們開始之前，您必須確定您的憑證符合這些需求：
- [有效期自] 屬性的憑證和之前的有效憑證的屬性之後，必須是目前系統時間。
- 憑證必須是為了伺服器驗證而準備的。 這需要指定伺服器驗證 (1.3.6.1.5.5.7.3.1) 憑證的增強金鑰使用方法屬性。
- 必須使用 AT_KEYEXCHANGE KeySpec 選項來建立憑證。 通常，憑證的金鑰使用方法屬性 (KEY_USAGE) 也會包括金鑰編密 (CERT_KEY_ENCIPHERMENT_KEY_USAGE)。
- 憑證的 Subject 屬性必須指出一般名稱 (CN)，做為主機名稱或伺服器電腦的完整的網域名稱 (FQDN) 會相同。 附註： 支援萬用字元憑證。 

## <a name="overview"></a>概觀
TLS 用來加密從用戶端應用程式的連線[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 如果設定正確，TLS 提供隱私權與資料完整性，以用戶端與伺服器之間的通訊。  TLS 連線可以是用戶端 intiated 或伺服器 initited。 


## <a name="client-initiated-encryption"></a>用戶端起始加密 
- **產生憑證**（/CN 應符合您的 SQL Server 主機完整網域名稱）

> [!NOTE]
> 此範例中，我們會使用自我簽署憑證，這應該不用於生產案例中。 您應該使用的 CA 憑證。 

        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **設定 SQL Server**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0 

- **註冊用戶端電腦 （Windows、 Linux 或 macOS） 上的憑證**

    -   如果您使用 CA 簽署的憑證，您必須將憑證授權單位 (CA) 憑證，而不是使用者憑證複製到用戶端電腦。 
    -   如果您只使用自我簽署的憑證將.pem 檔案複製到下列資料夾發佈到個別和執行命令，讓它們 
        - **Ubuntu** ： 將憑證複製到```/usr/share/ca-certificates/```.crt 重新命名延伸模組會使用以 dpkg 重新設定 ca 憑證以便讓它成為系統 CA 憑證。 
        - **RHEL** ： 將憑證複製到```/etc/pki/ca-trust/source/anchors/```使用```update-ca-trust```以便讓它成為系統 CA 憑證。
        - **SUSE** ： 將憑證複製到```/usr/share/pki/trust/anchors/```使用```update-ca-certificates```啟用就像系統 CA 憑證。
        - **Windows**:.pem 檔案，做為憑證以目前使用者]-> [匯入信任的根憑證授權單位]-> [憑證
        - **macOS**: 
           - 複製到憑證```/usr/local/etc/openssl/certs```
           - 執行下列命令，以取得雜湊值：```/usr/local/Cellar/openssql/1.0.2l/openssql x509 -hash -in mssql.pem -noout```
           - 將憑證重新命名為值。 例如： ```mv mssql.pem dc2dd900.0```。 請確定 dc2dd900.0 處於```/usr/local/etc/openssl/certs```
    
-   **範例連接字串** 

    - **[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]**   
  ![SSMS 連接對話方塊](media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "SSMS 連接對話方塊")  
  
    - **SQLCMD** 

            sqlcmd  -S <sqlhostname> -N -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=True; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=Yes; TrustServerCertificate=no;" 
    - **JDBC** 
    
            "encrypt=true; trustServerCertificate=false;" 

## <a name="server-initiated-encryption"></a>伺服器會起始加密 

- **產生憑證**（/CN 應符合您的 SQL Server 主機完整網域名稱）
        
        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **設定 SQL Server**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 1 
        
-   **範例連接字串** 

    - **SQLCMD**

            sqlcmd  -S <sqlhostname> -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=False; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=no; TrustServerCertificate=no;"  
    - **JDBC** 
    
            "encrypt=false; trustServerCertificate=false;" 
            
> [!NOTE]
> 設定**TrustServerCertificate**為 True，如果用戶端無法連線到 CA 以驗證憑證的真確性

## <a name="common-connection-errors"></a>一般連接錯誤  

|錯誤訊息 |Fix |
|--- |--- |
|不受信任授權單位所核發的憑證鏈結。  |當用戶端無法驗證 SQL Server 的 TLS 信號交換期間出示的憑證上的簽章時，就會發生此錯誤。 請確定用戶端所信任是[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]直接，憑證或 CA 簽署的 SQL Server 憑證。 |
|目標主體名稱不正確。  |請確定 SQL 伺服器的憑證上的 [一般名稱] 欄位符合用戶端的連接字串中指定的伺服器名稱。 |  
|遠端主機已強制關閉現有的連接。 |當用戶端不支援所需的 SQL Server 的 TLS 通訊協定版本，就會發生此錯誤。 例如，如果[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]已設定為需要 TLS 1.2，請確定您的用戶端也支援 TLS 1.2 通訊協定。 |
| | |   

