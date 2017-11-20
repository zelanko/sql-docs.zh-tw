---
title: "catalog.cleanup_server_execution_keys |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a79f1006-54e8-4cbf-96f8-5ed143ebb830
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 172925d5a63aa831881b6a6325f0dbcbccd4dd56
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcleanupserverexecutionkeys"></a>catalog.cleanup_server_execution_keys
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  從 SSISDB 資料庫中卸除憑證及對稱金鑰。  
  
## <a name="syntax"></a>語法  
  
```sql
catalog.cleanup_server_execution_keys [ @cleanup_flag = ] cleanup_flag ,  
[ @delete_batch_size = ] delete_batch_size  
```  
  
## <a name="arguments"></a>引數  
 [ @cleanup_flag =] *cleanup_flag*  
 指出是否執行層級 （1） 或專案層級 （2） 憑證和對稱金鑰是要卸除。  
  
 只有 SERVER_OPERATION_ENCRYPTION_LEVEL 設定為 PER_EXECUTION (1) 時，請使用執行層級 (1)。  
  
 只有 SERVER_OPERATION_ENCRYPTION_LEVEL 設定為 PER_PROJECT (2) 時，請使用專案層級 (2)。 僅針對已刪除，並具有已清除的作業記錄檔的專案會卸除憑證和對稱金鑰。  
  
 [ @delete_batch_size =] *delete_batch_size*  
 索引鍵和憑證是要卸除的數字。 預設值為 1000年。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 代表成功，1 表示失敗。  
  
## <a name="result-sets"></a>結果集  
 無。  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   讀取和執行專案的權限和 （適用），讀取權限參考的環境。  
  
-   中的成員資格**ssis_admin**資料庫角色。  
  
-   成員資格**sysadmin**伺服器角色。  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 這個預存程序會引發錯誤，依下列情況：  
  
-   有一或多個作用中的作業，SSISDB 資料庫中。  
  
-   SSISDB 資料庫不是處於單一使用者模式。  
  
## <a name="remarks"></a>備註  
 SQL Server 2012 Service Pack 2 新增至 SERVER_OPERATION_ENCRYPTION_LEVEL 屬性**internal.catalog_properties**資料表。 此屬性具有兩個可能值：  
  
-   **(1) PER_EXECUTION** -憑證和對稱金鑰用於保護機密的執行中參數，並執行記錄會建立每次執行。 這是預設值。 您可能會遇到效能問題 （死結，失敗的維護工作等...） 在生產環境中因為每次執行會產生憑證/金鑰。 不過，這項設定會提供較高的安全性比其他值 (2)。  
  
-   **(2) PER_PROJECT** – 每個專案建立的憑證和對稱金鑰用於保護敏感性參數。 這可讓您更佳的效能比 PER_EXECUTION 層級因為金鑰和憑證會產生一次的專案，而不是每次執行。  
  
 您必須執行[catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md)預存程序，從 1 到 2 （或） 從 1 到 2，才能變更 SERVER_OPERATION_ENCRYPTION_LEVEL。 執行這個預存程序之前，請執行下列動作：  
  
1.  請確定 OPERATION_CLEANUP_ENABLED 屬性的值設定為 TRUE 的[catalog.catalog_properties &#40;SSISDB 資料庫 &#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)資料表。  
  
2.  設定為單一使用者模式的 Integration Services 資料庫 (SSISDB)。 在 SQL Server Management Studio，啟動 SSISDB 資料庫屬性 對話方塊、 切換到 選項 索引標籤，並限制存取 屬性設定為單一使用者模式 (SINGLE_USER)。 執行 cleanup_server_log 之後預存程序，會設定屬性值設回原始值。  
  
3.  執行預存程序[catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md)。  
  
4.  現在，請繼續並變更 SERVER_OPERATION_ENCRYPTION_LEVEL 屬性中的值[catalog.catalog_properties &#40;SSISDB 資料庫 &#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)資料表。  
  
5.  執行預存程序[catalog.cleanup_server_execution_keys](../../integration-services/system-stored-procedures/catalog-cleanup-server-execution-keys.md)清除憑證金鑰從 SSISDB 資料庫。 從 SSISDB 資料庫卸除憑證和金鑰可能需要很長的時間，讓它應該定期在離峰時間執行。  
  
     您可以指定的範圍或層級 （執行與專案） 和刪除的索引鍵數目。 刪除的預設批次大小為 1000年。 當您將層級設定為 2 時，金鑰和憑證會才刪除相關的專案已被刪除。  
  
 如需詳細資訊，請參閱下列知識庫文件。 [修正： 儲存在 SQL Server 2012 中的 SSISDB 作為您的部署時的效能問題](http://support.microsoft.com/kb/2972285)  
  
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
  
  

