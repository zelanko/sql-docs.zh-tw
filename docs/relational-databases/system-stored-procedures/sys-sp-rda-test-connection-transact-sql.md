---
title: sys.sp_rda_test_connection (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_test_connection
- sys.sp_rda_test_connection_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_test_connection stored procedure
ms.assetid: e2ba050c-d7e3-4f33-8281-c9b525b4edb4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a63a88e24f62ba9d8a4a70107663ab2d585f4640
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061795"
---
# <a name="syssprdatestconnection-transact-sql"></a>sys.sp_rda_test_connection & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  測試從 SQL Server 連接到遠端 Azure 伺服器和報告可能會導致資料移轉的問題。  
  
## <a name="syntax"></a>語法  
  
```  
  
EXECUTE sys.sp_rda_test_connection  
   @database_name = N'db_name',   
   @server_address = N'azure_server_fully_qualified_address',  
   @azure_username = N'azure_username',   
   @azure_password = N'azure_password',  
   @credential_name = N'credential_name'  
  
```  
  
## <a name="arguments"></a>引數  
 @database_name = N'*db_name*'  
 已啟用 Stretch 的 SQL Server 資料庫的名稱。 這個參數是選擇性的。  
  
 @server_address = N'*azure_server_fully_qualified_address*'  
 Azure 伺服器的完整的位址。  
  
-   如果您提供的值 **@database_name** ，但指定的資料庫不是已啟用延展功能，則您必須提供值給 **@server_address** 。  
  
-   如果您提供的值 **@database_name** ，和指定的資料庫已啟用延展功能，則您不需要提供值給 **@server_address** 。 如果您提供的值 **@server_address** 、 預存程序會忽略它，並使用已現有 Azure 伺服器相關聯的已啟用 Stretch 的資料庫。  
  
 @azure_username = N'*azure_username*  
 遠端 Azure 伺服器使用者名稱。  
  
 @azure_password = N'*azure_password*'  
 遠端 Azure 伺服器的密碼。  
  
 @credential_name = N'*credential_name*'  
 而不是提供使用者名稱和密碼，您可以提供已啟用 Stretch 的資料庫中儲存認證的名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 中的案例**成功**sp_rda_test_connection 嚴重性 EX_INFO 傳回錯誤 14855 （STRETCH_MAJOR、 STRETCH_CONNECTION_TEST_PROC_SUCCEEDED），成功傳回碼。  
  
 中的案例**失敗**、 sp_rda_test_connection 嚴重性 EX_USER 傳回錯誤 14856 （STRETCH_MAJOR、 STRETCH_CONNECTION_TEST_PROC_FAILED） 和錯誤傳回碼。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|link_state|ssNoversion|下列的值，對應至值的其中一個**link_state_desc**。<br /><br /> -   0<br />-   1<br />-   2<br />-   3<br />-   4|  
|link_state_desc|varchar(32)|下列的值，這會對應到上述其中一個值**link_state**。<br /><br /> -狀況良好<br />     SQL Server 與遠端 Azure 伺服器狀況良好。<br />-   ERROR_AZURE_FIREWALL<br />     Azure 防火牆阻止 SQL Server 與遠端 Azure 伺服器之間的連結。<br />-ERROR_NO_CONNECTION<br />     SQL Server 無法建立連線到遠端 Azure 伺服器。<br />-   ERROR_AUTH_FAILURE<br />     發生驗證錯誤會導致 SQL Server 與遠端 Azure 伺服器之間的連結。<br />-錯誤<br />     不是驗證問題、 連線問題或防火牆問題的錯誤導致 SQL Server 與遠端 Azure 伺服器之間的連結。|  
|error_number|ssNoversion|錯誤數目。 如果沒有發生錯誤，則此欄位會是 NULL。|  
|error_message|nvarchar(1024)|錯誤訊息。 如果沒有發生錯誤，則此欄位會是 NULL。|  
  
## <a name="permissions"></a>Permissions  
 需要 db_owner 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="check-the-connection-from-sql-server-to-the-remote-azure-server"></a>請檢查 SQL Server 遠端 Azure 伺服器的連線  
  
```sql  
EXECUTE sys.sp_rda_test_connection @database_name = N'<Stretch-enabled database>'  
GO  
  
```  
  
 結果會顯示 SQL Server 無法連接到遠端 Azure 伺服器。  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|2|ERROR_NO_CONNECTION|*\<連接相關的錯誤號碼 >*|*\<連接相關的錯誤訊息 >*|  
  
### <a name="check-the-azure-firewall"></a>請檢查 Azure 防火牆  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 結果會顯示 Azure 防火牆會防止 SQL Server 與遠端 Azure 伺服器之間的連結。  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|1|ERROR_AZURE_FIREWALL|*\<防火牆相關的錯誤號碼 >*|*\<防火牆相關的錯誤訊息 >*|  
  
### <a name="check-authentication-credentials"></a>請檢查驗證認證  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 結果會顯示發生驗證錯誤，導致 SQL Server 與遠端 Azure 伺服器之間的連結。  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|3|ERROR_AUTH_FAILURE|*\<驗證相關的錯誤號碼 >*|*\<驗證相關的錯誤訊息 >*|  
  
### <a name="check-the-status-of-the-remote-azure-server"></a>檢查遠端 Azure 伺服器的狀態  
  
```sql  
USE <SQL Server database>  
GO  
EXECUTE sys.sp_rda_test_connection   
    @server_address = N'<server name>.database.windows.net',   
    @azure_username = N'<user name>',   
    @azure_password = N'<password>'  
GO  
  
```  
  
 結果會顯示連線狀況良好，且您可以針對指定的資料庫啟用 Stretch Database。  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|0|HEALTHY|NULL|NULL|  
  
  
