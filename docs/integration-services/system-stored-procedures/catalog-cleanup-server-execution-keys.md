---
title: catalog.cleanup_server_execution_keys | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a79f1006-54e8-4cbf-96f8-5ed143ebb830
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 619fea014d695cb4601eaf876dcca0add3604f2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110476"
---
# <a name="catalogcleanupserverexecutionkeys"></a>catalog.cleanup_server_execution_keys 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  從 SSISDB 資料庫中卸除憑證及對稱金鑰。  
  
## <a name="syntax"></a>語法  
  
```sql
catalog.cleanup_server_execution_keys [ @cleanup_flag = ] cleanup_flag ,  
[ @delete_batch_size = ] delete_batch_size  
```  
  
## <a name="arguments"></a>引數  
 [ @cleanup_flag = ] *cleanup_flag*  
 指出要捨棄執行層級 (1) 還是專案層級 (2) 憑證和對稱金鑰。  
  
 只有在 SERVER_OPERATION_ENCRYPTION_LEVEL 設定為 PER_EXECUTION (1) 時，才使用執行層級 (1)。  
  
 只有在 SERVER_OPERATION_ENCRYPTION_LEVEL 設定為 PER_PROJECT (2) 時，才使用專案層級 (2)。 只針對已刪除的專案和已清除作業記錄的專案，捨棄其憑證和對稱金鑰。  
  
 [ @delete_batch_size = ] *delete_batch_size*  
 要捨棄的金鑰和憑證數目。 預設值為 1000。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 表示成功，1 則表示失敗。  
  
## <a name="result-sets"></a>結果集  
 無。  
  
## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   專案的 READ 與 EXECUTE 權限，以及參考環境的 READ 權限 (如果適用的話)。  
  
-   **ssis_admin** 資料庫角色中的成員資格。  
  
-   **sysadmin** 伺服器角色的成員資格。  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 在下列情況下，此預存程序會引發錯誤：  
  
-   SSISDB 資料庫中有一或多個作用中的作業。  
  
-   SSISDB 資料庫未處於單一使用者模式。  
  
## <a name="remarks"></a>Remarks  
 SQL Server 2012 Service Pack 2 已將 SERVER_OPERATION_ENCRYPTION_LEVEL 屬性新增至 **internal.catalog_properties** 資料表。 此屬性有兩個可能的值：  
  
-   **PER_EXECUTION (1)** - 會針對每次執行建立憑證和對稱金鑰，以用於保護機密的執行參數和執行記錄。 這是預設值。 您可能會在生產環境中遇到效能問題 (鎖死、維護作業失敗等等)，因為每次執行時都會產生憑證/金鑰。 不過，此設定所提供的安全性層級高於另一個值 (2)。  
  
-   **PER_PROJECT (2)** - 會針對每個專案建立憑證和對稱金鑰，以用於保護敏感性 參數。 這可讓您擁有的效能優於 PER_EXECUTION 層級，因為金鍵和憑證只會針對專案產生一次，而不是每次執行都產生一次。  
  
 您必須先執行 [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md) 預存程序，才能將 SERVER_OPERATION_ENCRYPTION_LEVEL 從 1 變更為 2 (或) 從 2 變更為 1。 執行此預存程序之前，請執行下列動作：  
  
1.  確定 [catalog.catalog_properties &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) 資料表中的 OPERATION_CLEANUP_ENABLED 屬性值設定為 TRUE。  
  
2.  將 Integration Services 資料庫 (SSISDB) 設為單一使用者模式。 在 SQL Server Management Studio 中，啟動 SSISDB 的 [資料庫屬性] 對話方塊，再切換至 [選項] 索引標籤，然後將 [限制存取] 屬性設為單一使用者模式 (SINGLE_USER)。 執行 cleanup_server_log 預存程序之後，請將屬性值設回原始值。  
  
3.  執行 [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md) 預存程序。  
  
4.  現在，請繼續變更 [catalog.catalog_properties &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) 資料表中的 SERVER_OPERATION_ENCRYPTION_LEVEL 屬性值。  
  
5.  執行 [catalog.cleanup_server_execution_keys](../../integration-services/system-stored-procedures/catalog-cleanup-server-execution-keys.md) 預存程序，以清除 SSISDB 資料庫中的憑證金鑰。 捨棄 SSISDB 資料庫中的憑證和金鑰可能需要很長的時間，因此您應該在離峰期間定期執行這項作業。  
  
     您可以指定範圍或層級 (執行/專案) 以及要刪除的金鑰數目。 刪除的預設批次大小是 1000。 如果您將層級設定為 2，則只有在刪除相關的專案時，才會刪除金鑰和憑證。  
  
 如需詳細資訊，請參閱下列知識庫文章。 [修正：當您在 SQL Server 2012 中使用 SSISDB 作為部署存放區時的效能問題](https://support.microsoft.com/kb/2972285)  
  
## <a name="example"></a>範例  
 下列範例會呼叫 cleanup_server_execution_keys 預存程序。  
  
```sql  
USE [SSISDB]  
GO  
  
DECLARE@return_value int  
  
EXEC@return_value = [internal].[cleanup_server_execution_keys]  
@cleanup_flag = 1,  
@delete_batch_size = 500  
  
SELECT'Return Value' = @return_value  
  
GO  
```  
  
  
