---
title: 允許資料庫鏡像端點使用傳入連接的憑證（Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- certificates [SQL Server], database mirroring
- inbound connections
- database mirroring [SQL Server], security
ms.assetid: 5d48bb98-61f0-4b99-8f1a-b53f831d63d0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3f70ddfc241a902a59dff989323a75b17f7af55e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62807556"
---
# <a name="allow-a-database-mirroring-endpoint-to-use-certificates-for-inbound-connections-transact-sql"></a>允許資料庫鏡像端點使用傳入連接的憑證 (Transact-SQL)
  此主題描述設定伺服器執行個體，以使用憑證來驗證資料庫鏡像之傳入連接的步驟。 在設定傳入連接之前，您必須先在每一個伺服器執行個體上設定傳出連接。 如需詳細資訊，請參閱 [允許資料庫鏡像端點使用輸出連線的憑證 &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md)。  
  
 設定傳入連接的程序，包括下列一般步驟：  
  
1.  為其他系統建立登入。  
  
2.  為該登入建立使用者。  
  
3.  取得另一個伺服器執行個體的鏡像端點的憑證。  
  
4.  使憑證與步驟 2 所建立的使用者產生關聯。  
  
5.  將 CONNECT 權限授與登入，以連接該鏡像端點。  
  
 如果有見證，您也必須為它設定傳入連接。 這需要在兩個夥伴上設定見證的登入、使用者和憑證，反之亦然。  
  
 下列程序將詳細說明這些步驟。 對於每個步驟，此程序會提供在名為 HOST_A 的系統上設定伺服器執行個體的範例。 隨附的「範例」部分則針對名為 HOST_B 系統上的另一個伺服器執行個體示範相同的步驟。  
  
### <a name="to-configure-server-instances-for-inbound-mirroring-connections-on-host_a"></a>設定 (HOST_A 上) 傳入鏡像連接的伺服器執行個體  
  
1.  為其他系統建立登入。  
  
     下列範例在 HOST_A 之伺服器執行個體的 **master** 資料庫中，建立系統 HOST_B 的登入；在此範例中，登入名稱為 `HOST_B_login`。 以您自己的密碼取代範例密碼。  
  
    ```  
    USE master;  
    CREATE LOGIN HOST_B_login   
       WITH PASSWORD = '1Sample_Strong_Password!@#';  
    GO  
    ```  
  
     如需詳細資訊，請參閱 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)。  
  
     若要檢視此伺服器執行個體上的登入，您可以使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    SELECT * FROM sys.server_principals  
    ```  
  
     如需詳細資訊，請參閱 [sys.server_principals &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql)。  
  
2.  為該登入建立使用者。  
  
     下列範例為上一個步驟所建立的登入，建立使用者 `HOST_B_user`。  
  
    ```  
    USE master;  
    CREATE USER HOST_B_user FOR LOGIN HOST_B_login;  
    GO  
    ```  
  
     如需詳細資訊，請參閱 [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)。  
  
     若要檢視此伺服器執行個體上的使用者，您可以使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    SELECT * FROM sys.sysusers;  
    ```  
  
     如需詳細資訊，請參閱 [sys.sysusers &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysusers-transact-sql)。  
  
3.  取得另一個伺服器執行個體的鏡像端點的憑證。  
  
     如果在設定傳出連接前，您尚未這麼做，請為遠端伺服器執行個體的鏡像端點取得憑證副本。 若要這樣做，請依[允許資料庫鏡像端點使用傳出連接的憑證 &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md)中所述在該伺服器執行個體上備份憑證。 將憑證複製到另一個系統時，請使用安全複製方法。 務必將您所有的憑證小心保管。  
  
     如需詳細資訊，請參閱 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-certificate-transact-sql)。  
  
4.  使憑證與步驟 2 所建立的使用者產生關聯。  
  
     下列範例使 HOST_B 的憑證與它在 HOST_A 的使用者產生關聯。  
  
    ```  
    USE master;  
    CREATE CERTIFICATE HOST_B_cert  
       AUTHORIZATION HOST_B_user  
       FROM FILE = 'C:\HOST_B_cert.cer'  
    GO  
    ```  
  
     如需詳細資訊，請參閱 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)。  
  
     若要檢視此伺服器執行個體上的憑證，請使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    SELECT * FROM sys.certificates  
    ```  
  
     如需詳細資訊，請參閱 [sys.certificates &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-certificates-transact-sql)。  
  
5.  將 CONNECT 權限授與登入，以連接遠端鏡像端點。  
  
     例如，若要在 HOST_A 上授與權限給 HOST_B 上的遠端伺服器執行個體來連接到其本機登入 (也就是連接到 `HOST_B_login`)，請使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    USE master;  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [HOST_B_login];  
    GO  
    ```  
  
     如需詳細資訊，請參閱 [GRANT 端點權限 &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql)。  
  
 如此即完成為 HOST_B 設定憑證驗證來登入到 HOST_A。  
  
 接著，您必須為 HOST_B 上的 HOST_A 執行對等的傳入步驟。 這些步驟將在下一節＜範例＞中範例的傳入部分加以說明。  
  
## <a name="example"></a>範例  
 下列範例示範設定 HOST_B 的傳入連接。  
  
> [!NOTE]  
>  本例使用包含 HOST_A 憑證的憑證檔案，此 HOST_A 憑證是由[允許資料庫鏡像端點使用傳出連接的憑證 &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md) 中的程式碼片段所建立。  
  
```  
USE master;  
--On HOST_B, create a login for HOST_A.  
CREATE LOGIN HOST_A_login WITH PASSWORD = 'AStrongPassword!@#';  
GO  
--Create a user, HOST_A_user, for that login.  
CREATE USER HOST_A_user FOR LOGIN HOST_A_login  
GO  
--Obtain HOST_A certificate. (See the note   
--   preceding this example.)  
--Asscociate this certificate with the user, HOST_A_user.  
CREATE CERTIFICATE HOST_A_cert  
   AUTHORIZATION HOST_A_user  
   FROM FILE = 'C:\HOST_A_cert.cer';  
GO  
--Grant CONNECT permission for the server instance on HOST_A.  
GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO HOST_A_login  
GO  
```  
  
 如果您想要在具有自動容錯移轉的高安全性模式下執行，就必須重複相同的設定步驟，以便設定傳出和傳入連接的見證。  
  
 如需建立鏡像資料庫的相關資訊，包括 Transact-SQL 範例在內，請參閱[準備鏡像資料庫以進行鏡像 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)。  
  
 如需建立高效能模式工作階段的 Transact-SQL 範例，請參閱 [範例：使用憑證設定資料庫鏡像 &#40;Transact-SQL&#41;](example-setting-up-database-mirroring-using-certificates-transact-sql.md)。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 將憑證複製到另一個系統時，請使用安全複製方法。 務必將您所有的憑證小心保管。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫鏡像和 AlwaysOn 可用性群組的傳輸安全性 &#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md)   
 [GRANT 端點權限 &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql)   
 [設定加密鏡像資料庫](set-up-an-encrypted-mirror-database.md)   
 [資料庫鏡像端點 &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [疑難排解資料庫鏡像組態 &#40;SQL Server&#41;](troubleshoot-database-mirroring-configuration-sql-server.md)  
  
  
