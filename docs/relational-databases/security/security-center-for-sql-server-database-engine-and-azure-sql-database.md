---
title: SQL Server 和 Azure SQL Database 的安全性文件
description: 適用於 SQL Server 和 Azure SQL Database 的安全性和保護相關內容的參考。
ms.custom: seo-lt-2019
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- Security [SQL Server]
helpviewer_keywords:
- SQL Server, security
- security [SQL Server]
- database security [SQL Server]
- databases [SQL Server], security
ms.assetid: dfb39d16-722a-4734-94bb-98e61e014ee7
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e46a4a7cc107fb3d51f7f65130c3529290d54dfb
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/27/2020
ms.locfileid: "92678959"
---
# <a name="security-center-for-sql-server-database-engine-and-azure-sql-database"></a>SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  本頁提供的連結有助於您尋找所需之 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]中安全性與保護的相關資訊。  
  
 **圖例**  
  
 ![說明功能可用性圖示的圖例螢幕擷取畫面。](../performance/media/security-center-legend.PNG "security-center-legend")  
  
##  <a name="authentication-who-are-you"></a><a name="Who"></a> 驗證：您是誰？  
  
|||  
|-|-|  
|**由誰驗證？**<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: Windows 驗證<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證<br /><br /> :::image type="icon" source="../../relational-databases/security/media/security-center-sqldb.png"::: Azure Active Directory|由誰驗證？ (Windows 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])<br /><br /> [選擇驗證模式](../../relational-databases/security/choose-an-authentication-mode.md)<br /><br /> [使用 Azure Active Directory 驗證連線到 SQL 資料庫](/azure/azure-sql/database/authentication-aad-overview)|  
|**驗證位置？**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 在 master 資料庫上：登入和 DB 使用者<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 在使用者資料庫上：已包含的 DB 使用者|在 master 資料庫進行驗證 (登入和資料庫使用者)<br /><br /> [建立 SQL Server 登入](../../relational-databases/security/authentication-access/create-a-login.md)<br /><br /> [管理資料庫和 Azure SQL Database 中的登入](/previous-versions/azure/ee336235(v=azure.100))<br /><br /> [建立資料庫使用者](../../relational-databases/security/authentication-access/create-a-database-user.md)<br /><br /> <br /><br /> 在使用者資料庫進行驗證<br /><br /> [自主資料庫使用者 - 讓資料庫具有可攜性](../../relational-databases/security/contained-database-users-making-your-database-portable.md)|  
|**使用其他身分識別**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 認證<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: 以另一個登入的方式執行<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 以另一個資料庫使用者的身分執行|[認證 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)<br /><br /> [以另一個登入的方式執行](../../t-sql/statements/execute-as-transact-sql.md)<br /><br /> [以另一個資料庫使用者的身分執行](../../t-sql/statements/execute-as-transact-sql.md)|  
  
##  <a name="authorization-what-can-you-do"></a><a name="What"></a> 授權：您可以做什麼？  
  
|||  
|-|-|  
|**授與、撤銷和拒絕權限**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 安全性實體類別<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: 細微伺服器權限<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 細微資料庫權限|[權限階層 &#40;Database Engine&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)<br /><br /> [權限](../../relational-databases/security/permissions-database-engine.md)<br /><br /> [安全性實體](../../relational-databases/security/securables.md)<br /><br /> [資料庫引擎權限使用者入門](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)|  
|**安全性角色**<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: 伺服器層級角色<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 資料庫層級角色|[伺服器層級角色](../../relational-databases/security/authentication-access/server-level-roles.md)<br /><br /> [資料庫層級角色](../../relational-databases/security/authentication-access/database-level-roles.md)|  
|**限制對選取的資料元素的資料存取**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 以檢視/程序限制資料存取<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 資料列層級安全性<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 動態資料遮罩<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 簽署物件|限制資料存取使用 [檢視](../../relational-databases/views/views.md) 和 [程序](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)<br /><br /> [資料列層級安全性 (SQL Server)](../../relational-databases/security/row-level-security.md)<br /><br /> [資料列層級安全性 (Azure SQL Database)](./row-level-security.md)<br /><br /> [動態資料遮罩 (SQL Server)](../../relational-databases/security/dynamic-data-masking.md)<br /><br /> [動態資料遮罩 (Azure SQL Database)](/azure/azure-sql/database/dynamic-data-masking-overview)<br /><br /> [簽署物件](../../t-sql/statements/add-signature-transact-sql.md)|  
  
##  <a name="encryption-storing-secret-data"></a><a name="Encrypt"></a> 加密：儲存機密資料  
  
|||  
|-|-|  
|**加密檔案**<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: BitLocker 加密 (磁碟機層級)<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: NTFS 加密 (資料夾層級)<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 透明資料加密 (檔案層級)<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 備份加密 (檔案層級)|[BitLocker (磁碟機層級)](https://support.microsoft.com/kb/2855131)<br /><br /> [NTFS 加密 (資料夾層級)](/previous-versions/tn-archive/dd163562(v=technet.10))<br /><br /> [透明資料加密 (檔案層級)](../../relational-databases/security/encryption/transparent-data-encryption.md)<br /><br /> [備份加密 (檔案層級)](../../relational-databases/backup-restore/backup-encryption.md)|  
|**加密的來源**<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: 可延伸金鑰管理模組<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: 儲存在 Azure Key Vault 的金鑰<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Always Encrypted|[可延伸金鑰管理模組](../../relational-databases/security/encryption/extensible-key-management-ekm.md)<br /><br /> [儲存在 Azure 金鑰保存庫的金鑰](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)<br /><br /> [一律加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md)|  
|**資料行、資料和金鑰加密**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 用憑證來加密<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 用對稱金鑰來加密<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 用非對稱金鑰來加密<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 用複雜密碼來加密|[加密憑證](../../t-sql/functions/encryptbycert-transact-sql.md)<br /><br /> [用非對稱金鑰來加密](../../t-sql/functions/encryptbyasymkey-transact-sql.md)<br /><br /> [用對稱金鑰來加密](../../t-sql/functions/encryptbykey-transact-sql.md)<br /><br /> [用複雜密碼來加密](../../t-sql/functions/encryptbypassphrase-transact-sql.md)<br /><br /> [加密資料行](../../relational-databases/security/encryption/encrypt-a-column-of-data.md)|  
  
##  <a name="connection-security-restricting-and-securing"></a><a name="Connect"></a> 連線安全性：限制和保護  
  
|||  
|-|-|  
|**防火牆保護**<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: Windows 防火牆設定<br /><br /> :::image type="icon" source="../../relational-databases/security/media/security-center-sqldb.png"::: Azure 服務防火牆設定<br /><br /> :::image type="icon" source="../../relational-databases/security/media/security-center-sqldb.png"::: 資料庫防火牆設定|[設定用於 Database Engine 存取的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)<br /><br /> [Azure SQL Database 防火牆設定](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)<br /><br /> [Azure 服務的防火牆設定](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)|  
|**在傳輸過程中的資料加密**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 強制的 SSL 連線<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: 選用的 SSL 連線|[啟用資料庫引擎的加密連接](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)<br /><br /> [啟用資料庫引擎的加密連線](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)、[網路安全性](/azure/sql-database/sql-database-security-best-practice#network-security) <br /><br /> [Microsoft SQL Server 的 TLS 1.2 支援](https://support.microsoft.com/kb/3135244)|  
  
##  <a name="auditing-recording-access"></a><a name="Audit"></a> 稽核：錄製存取權  
  
|||  
|-|-|  
|**自動化稽核**<br /><br /> :::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 稽核 (伺服器和 DB 層級)<br /><br /> :::image type="icon" source="../../relational-databases/security/media/security-center-sqldb.png"::: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 稽核 (資料庫層級)<br /><br /> :::image type="icon" source="../../relational-databases/security/media/security-center-sqldb.png"::: 偵測威脅| <br /><br /> [SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)<br /><br /> [SQL 資料庫稽核](/azure/azure-sql/database/auditing-overview)<br /><br /> [開始使用 SQL Database 進階威脅防護](/azure/azure-sql/database/threat-detection-configure) <br /><br /> [SQL Database 弱點評量](/azure/sql-database/sql-vulnerability-assessment) |  
|**自訂稽核**<br /><br /> :::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: 觸發程序|實作自訂的稽核：建立 [DDL Triggers](../../relational-databases/triggers/ddl-triggers.md) 和 [DML Triggers](../../relational-databases/triggers/dml-triggers.md)|  
|**遵循**<br /><br /> :::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: 合規性|SQL Server:<br />                        [Common Criteria](https://go.microsoft.com/fwlink/?LinkId=616319)<br /><br /> SQL Database：<br />                        [Microsoft Azure Trust Center:Compliance by Feature](https://azure.microsoft.com/support/trust-center/services/) (Microsoft Azure 信任中心：功能符合規範的狀況)|  
  
##  <a name="sql-injection"></a><a name="SQLInjection"></a> SQL 資料隱碼  
 SQL 插入式攻擊是指將惡意程式碼插入字串中，然後將這些字串傳遞至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 進行剖析和執行。 應該檢閱建構 SQL 陳述式之任何程序的資料隱碼弱點，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會執行所接收之所有語法有效的查詢。 所有的資料庫系統都有遭到 SQL 插入式攻擊的風險，且查詢 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的應用程式會導入許多漏洞。 您可以透過預存程序和參數化命令、避免動態 SQL 以及限制所有使用者的權限來防堵 SQL 插入式攻擊。  如需詳細資訊，請參閱 [SQL 插入](../../relational-databases/security/sql-injection.md)。  
  
 應用程式設計人員的其他連結︰  
  
-   [SQL Server 中的應用程式安全性案例](/dotnet/framework/data/adonet/sql/application-security-scenarios-in-sql-server)  
  
-   [在 SQL Server 撰寫安全動態 SQL](/dotnet/framework/data/adonet/sql/writing-secure-dynamic-sql-in-sql-server)  
  
-   [How To:Protect From SQL Injection in ASP.NET](/previous-versions/msp-n-p/ff648339(v=pandp.10)) (如何：在 ASP.NET 中防止 SQL 資料隱碼)  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎權限使用者入門](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [保護 SQL Server 的安全](../../relational-databases/security/securing-sql-server.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [SQL Server 憑證與非對稱金鑰](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)   
 [SQL Server 加密](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [介面區組態](../../relational-databases/security/surface-area-configuration.md)   
 [增強式密碼](../../relational-databases/security/strong-passwords.md)   
 [TRUSTWORTHY 資料庫屬性](../../relational-databases/security/trustworthy-database-property.md)   
 [Database Engine 功能及工作](../../sql-server/what-s-new-in-sql-server-ver15.md)  
 [保護 SQL Server 智慧財產權](../../relational-databases/security/protecting-your-sql-server-intellectual-property.md)   
  
[!INCLUDE[get-help-security](../../includes/get-help-security.md)]