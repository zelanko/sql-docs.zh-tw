---
title: sys.databases sp_rda_test_connection （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 69b3b9eae6c292b9501dfbe74b84d7399304a291
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305159"
---
# <a name="syssp_rda_test_connection-transact-sql"></a>sys.databases sp_rda_test_connection （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  測試從 SQL Server 到遠端 Azure 伺服器的連線，並報告可能導致資料移轉無法進行的問題。  
  
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
 @database_name = N '*db_name*'  
 已啟用延展功能的 SQL Server 資料庫名稱。 這個參數是選擇性的。  
  
 @server_address = N '*azure_server_fully_qualified_address*'  
 Azure 伺服器的完整位址。  
  
-   如果您為 **\@database_name**提供值，但指定的資料庫未啟用 Stretch，則您必須提供 **\@server_address**的值。  
  
-   如果您為 **\@database_name**提供值，而且指定的資料庫已啟用 Stretch，則您不需要提供 **\@server_address**的值。 如果您為 **\@server_address**提供值，則預存程式會忽略它，並使用已與已啟用延展功能的資料庫相關聯的現有 Azure 伺服器。  
  
 @azure_username = N '*azure_username*  
 遠端 Azure 伺服器的使用者名稱。  
  
 @azure_password = N '*azure_password*'  
 遠端 Azure 伺服器的密碼。  
  
 @credential_name = N '*credential_name*'  
 除了提供使用者名稱和密碼之外，您還可以提供儲存在已啟用 Stretch 之資料庫中的認證名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 如果**成功**，sp_rda_test_connection 會傳回錯誤14855（STRETCH_MAJOR，STRETCH_CONNECTION_TEST_PROC_SUCCEEDED），嚴重性 EX_INFO 和成功傳回碼。  
  
 萬一**發生失敗**，sp_rda_test_connection 會傳回錯誤14856（STRETCH_MAJOR，STRETCH_CONNECTION_TEST_PROC_FAILED），嚴重性 EX_USER 和錯誤傳回碼。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|[名稱]|描述|  
|-----------------|---------------|-----------------|  
|link_state|整數|下列其中一個值，對應至**link_state_desc**的值。<br /><br /> -0<br />-1<br />-2<br />-3<br />-4|  
|link_state_desc|Varchar （32）|下列其中一個值，對應至**link_state**前面的值。<br /><br /> -狀況良好<br />     SQL Server 和遠端 Azure 伺服器之間的狀況良好。<br />-ERROR_AZURE_FIREWALL<br />     Azure 防火牆會阻止 SQL Server 和遠端 Azure 伺服器之間的連結。<br />-ERROR_NO_CONNECTION<br />     SQL Server 無法建立與遠端 Azure 伺服器的連接。<br />-ERROR_AUTH_FAILURE<br />     驗證失敗，導致 SQL Server 和遠端 Azure 伺服器之間的連結無法使用。<br />-錯誤<br />     不是驗證問題、連線問題或防火牆問題的錯誤，導致 SQL Server 和遠端 Azure 伺服器之間的連結無法使用。|  
|error_number|整數|錯誤的數目。 如果沒有錯誤，此欄位會是 Null。|  
|error_message|nvarchar(1024)|錯誤訊息。 如果沒有錯誤，此欄位會是 Null。|  
  
## <a name="permissions"></a>Permissions  
 需要 db_owner 許可權。  
  
## <a name="examples"></a>範例  
  
### <a name="check-the-connection-from-sql-server-to-the-remote-azure-server"></a>檢查從 SQL Server 到遠端 Azure 伺服器的連線  
  
```sql  
EXECUTE sys.sp_rda_test_connection @database_name = N'<Stretch-enabled database>'  
GO  
  
```  
  
 結果顯示 SQL Server 無法連接到遠端 Azure 伺服器。  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|2|ERROR_NO_CONNECTION|*\<連接相關的錯誤號碼 >*|*\<連接相關的錯誤訊息 >*|  
  
### <a name="check-the-azure-firewall"></a>檢查 Azure 防火牆  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 結果顯示 Azure 防火牆會阻止 SQL Server 和遠端 Azure 伺服器之間的連結。  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|1|ERROR_AZURE_FIREWALL|*\<防火牆相關的錯誤號碼 >*|*\<防火牆相關的錯誤訊息 >*|  
  
### <a name="check-authentication-credentials"></a>檢查驗證認證  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 結果顯示驗證失敗，導致 SQL Server 和遠端 Azure 伺服器之間的連結無法使用。  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|3|ERROR_AUTH_FAILURE|*\<與驗證相關的錯誤號碼 >*|*\<與驗證相關的錯誤訊息 >*|  
  
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
  
 結果顯示連線狀況良好，而且您可以為指定的資料庫啟用 Stretch Database。  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|0|HEALTHY|NULL|NULL|  
  
  
