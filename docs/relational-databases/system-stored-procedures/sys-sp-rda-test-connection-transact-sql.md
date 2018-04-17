---
title: sys.sp_rda_test_connection (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_test_connection
- sys.sp_rda_test_connection_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_test_connection stored procedure
ms.assetid: e2ba050c-d7e3-4f33-8281-c9b525b4edb4
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 45ba48abca5372cde0e303bce431ef66b6e299df
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="syssprdatestconnection-transact-sql"></a>sys.sp_rda_test_connection (TRANSACT-SQL)
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
  
-   如果您提供的值**@database_name**，但是指定的資料庫未啟用 「 延展 」，則您必須提供值給**@server_address**。  
  
-   如果您提供的值**@database_name**，且指定的資料庫啟用 Stretch，然後您沒有提供值給**@server_address**。 如果您提供的值**@server_address**、 預存程序則會予以忽略並使用現有 Azure 伺服器已經相關聯的已啟用 Stretch 的資料庫。  
  
 @azure_username = N'*azure_username*  
 遠端 Azure 伺服器使用者名稱。  
  
 @azure_password = N'*azure_password*'  
 遠端 Azure 伺服器的密碼。  
  
 @credential_name = N'*credential_name*'  
 而不是提供使用者名稱和密碼，您可以提供認證，儲存在已啟用 Stretch 的資料庫名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 如果是**成功**、 sp_rda_test_connection 嚴重性 EX_INFO 傳回錯誤 14855 （STRETCH_MAJOR、 STRETCH_CONNECTION_TEST_PROC_SUCCEEDED） 和成功的傳回碼。  
  
 如果是**失敗**、 sp_rda_test_connection 嚴重性 EX_USER 傳回錯誤 14856 （STRETCH_MAJOR、 STRETCH_CONNECTION_TEST_PROC_FAILED） 和錯誤傳回碼。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|link_state|int|下列的值，對應至值的其中一個**link_state_desc**。<br /><br /> -   0<br />-   1<br />-   2<br />-   3<br />-   4|  
|link_state_desc|varchar （32)|下列的值，對應至前述其中一個值**link_state**。<br /><br /> -狀況良好<br />     SQL Server 與遠端 Azure 伺服器是狀況良好。<br />-ERROR_AZURE_FIREWALL<br />     Azure 防火牆阻止 SQL Server 與遠端 Azure 伺服器之間的連結。<br />-ERROR_NO_CONNECTION<br />     SQL Server 無法建立遠端 Azure 伺服器的連接。<br />-   ERROR_AUTH_FAILURE<br />     發生驗證錯誤會使得 SQL Server 與遠端 Azure 伺服器之間的連結。<br />-錯誤<br />     驗證問題、 連線問題或防火牆問題不是錯誤導致 SQL Server 與遠端 Azure 伺服器之間的連結。|  
|error_number|int|發生的錯誤數目。 如果沒有發生錯誤，此欄位為 NULL。|  
|error_message|nvarchar(1024)|錯誤訊息。 如果沒有發生錯誤，此欄位為 NULL。|  
  
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
|2|ERROR_NO_CONNECTION|*\<連接相關的錯誤號碼 >*|*\<與連接相關的錯誤訊息 >*|  
  
### <a name="check-the-azure-firewall"></a>請檢查 Azure 防火牆  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 結果會顯示 Azure 防火牆會使得 SQL Server 與遠端 Azure 伺服器之間的連結。  
  
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
  
 結果會顯示驗證錯誤會使得 SQL Server 與遠端 Azure 伺服器之間的連結。  
  
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
  
  
