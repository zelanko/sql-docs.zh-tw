---
title: 加密與 Linux 上 SQL Server 的連線
description: 此文章說明如何加密與 Linux 上 SQL Server 的連線。
ms.date: 01/30/2018
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
helpviewer_keywords:
- Linux, encrypted connections
ms.openlocfilehash: 3f658ba8723b142f37763ea8b4f0c8f7b0c5d0e1
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077293"
---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>加密與 Linux 上 SQL Server 的連線

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Linux 上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可以使用「傳輸層安全性」(TLS) 來加密在用戶端應用程式與 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體之間的網路傳輸的資料。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在 Windows 和 Linux 上支援相同的 TLS 通訊協定：TLS 1.2、1.1 及 1.0。 不過，設定 TLS 的步驟需視 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行環境作業系統而定。  

## <a name="requirements-for-certificates"></a>憑證需求 
開始之前，您必須確定憑證符合下列需求：
- 目前的系統時間必須在憑證的 [有效期限自] 屬性值之後，並且在憑證的 [有效期限至] 屬性值之前。
- 憑證必須是為了伺服器驗證而準備的。 這會要求憑證的 [增強金鑰使用方法] 屬性指定 [伺服器驗證 (1.3.6.1.5.5.7.3.1)]。
- 憑證必須使用 AT_KEYEXCHANGE 的 KeySpec 選項來建立。 通常，憑證的金鑰使用方法屬性 (KEY_USAGE) 也包括金鑰編密 (CERT_KEY_ENCIPHERMENT_KEY_USAGE)。
- 憑證的 [主旨] 屬性必須指出一般名稱 (CN) 與伺服器電腦的主機名稱或完整網域名稱 (FQDN) 相同。 注意：支援「萬用字元憑證」。

## <a name="configuring-the-openssl-libraries-for-use-optional"></a>設定要使用的 OpenSSL 程式庫 (選擇性)
您可以在 `/opt/mssql/lib/` 目錄中建立會參考應使用哪些 `libcrypto.so` 和 `libssl.so` 程式庫來進行加密的符號連結。 如果您想要強制 SQL Server 使用特定版本的 OpenSSL 而不是系統提供的預設值，這會相當有用。 如果這些符號連結不存在，SQL Server 就會在系統上載入預設設定的 OpenSSL 程式庫。

這些符號連結應該命名為 `libcrypto.so` 和 `libssl.so`，並放在 `/opt/mssql/lib/` 目錄中。

## <a name="overview"></a>概觀
TLS 可用來加密從用戶端應用程式到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的連線。 當已正確設定時，TLS 可為用戶端與伺服器之間的通訊同時提供私密性和安全性。  TLS 連線可以由用戶端起始或伺服器端起始。 

## <a name="client-initiated-encryption"></a>用戶端起始的加密 
- **產生憑證** (/CN 應該與您的 SQL Server 主機完整網域名稱相符)

> [!NOTE]
> 針對此範例，我們使用「自我簽署憑證」，這不應用於生產環境案例。 您應該使用 CA 憑證。 

        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **設定 SQL Server**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0 

- **在您的用戶端機器 (Windows、Linux 或 macOS) 上註冊憑證**

    -   如果您使用 CA 簽署的憑證，則必須將「憑證授權單位」(CA) 憑證而不是使用者憑證複製到用戶端機器。 
    -   如果您使用自我簽署憑證，只要將 .pem 檔案複製到下列發行版本的個別資料夾，並執行命令來啟用它們即可 
        - **Ubuntu**：將憑證複製到 ```/usr/share/ca-certificates/```，將副檔名重新命名為 .crt，使用 dpkg-reconfigure ca-certificates 來啟用它作為系統 CA 憑證。 
        - **RHEL**：將憑證複製到 ```/etc/pki/ca-trust/source/anchors/```，使用 ```update-ca-trust``` 來將其啟用成系統 CA 憑證。
        - **SUSE**：將憑證複製到 ```/usr/share/pki/trust/anchors/```，使用 ```update-ca-certificates``` 來啟用它作為系統 CA 憑證。
        - **Windows**：將 .pem 檔案匯入成 [目前的使用者] -> [受信任的根憑證授權單位] -> [憑證] 底下的憑證
        - **macOS**： 
           - 將憑證複製到 ```/usr/local/etc/openssl/certs```
           - 執行下列命令以取得雜湊值：```/usr/local/Cellar/openssql/1.0.2l/openssql x509 -hash -in mssql.pem -noout```
           - 將憑證重新命名成值。 例如：```mv mssql.pem dc2dd900.0```。 確定 dc2dd900.0 在 ```/usr/local/etc/openssl/certs``` 中
    
-   **範例連接字串** 

    - **[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]**   
  ![SSMS 連線對話方塊](media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "SSMS 連線對話方塊")  
  
    - **SQLCMD** 

            sqlcmd  -S <sqlhostname> -N -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=True; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=Yes; TrustServerCertificate=no;" 
    - **JDBC** 
    
            "encrypt=true; trustServerCertificate=false;" 

## <a name="server-initiated-encryption"></a>伺服器起始的加密 

- **產生憑證** (/CN 應該與您的 SQL Server 主機完整網域名稱相符)
        
        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **設定 SQL Server**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.key 
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
> 如果用戶端無法連線至 CA 來驗證憑證的真實性，請將 **TrustServerCertificate** 設定為 True

## <a name="common-connection-errors"></a>常見的連線錯誤  

|錯誤訊息 |修正 |
|--- |--- |
|此憑證鏈結是由不受信任的授權單位發出的。  |當用戶端無法驗證 SQL Server 在 TLS 信號交換期間所出示憑證上的簽章時，就會發生此錯誤。 確定用戶端直接信任 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 憑證，或信任簽署 SQL Server 憑證的 CA。 |
|目標主體名稱不正確。  |確定 SQL Server 憑證上的 [一般名稱] 欄位與用戶端連接字串中指定伺服器名稱相符。 |  
|遠端主機已強制關閉一個現有連線。 |當用戶端不支援 SQL Server 所需的 TLS 通訊協定版本時，就會發生此錯誤。 例如，如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 已設定為需要 TLS 1.2，請確定您的用戶端也支援 TLS 1.2 通訊協定。 |
| | |   
