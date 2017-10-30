---
title: "catalog.start_execution （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: f8663ff3-aa98-4dd8-b850-b21efada0b87
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 8edb51596198f27f00c1b78ddc8b3075ad035143
ms.contentlocale: zh-tw
ms.lasthandoff: 10/20/2017

---
# <a name="catalogstartexecution-ssisdb-database"></a>catalog.start_execution (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  啟動在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的執行執行個體。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.start_execution [@execution_id =] execution_id [, [@retry_count =] retry_count]  
```  
  
## <a name="arguments"></a>引數  
 [@execution_id =] *execution_id*  
 執行之執行個體的唯一識別碼。 *Execution_id*是**bigint**。
 
 [@retry_count =] *retry_count*  
 執行失敗時重試次數。 向外中執行時，才會生效。這個參數是選擇性的。 如果未指定，則會將其值設定為 0。 *Retry_count*是**int**。
  
## <a name="remarks"></a>備註  
 執行用來指定在封裝執行的單一執行個體期間封裝使用的參數值。 建立執行執行個體之後，在該執行執行個體啟動之前，對應的專案可能已重新部署。 在此情況下，執行執行個體參考的專案已過期。 無效的參考會導致失敗的預存程序。  
  
> [!NOTE]  
>  執行只能啟動一次。 若要開始執行的執行個體，它必須是處於已建立狀態 (值為`1`中**狀態**資料行[catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md)檢視)。  
  
## <a name="example"></a>範例  
 以下範例呼叫 catalog.create_execution 建立 Child1.dtsx 封裝執行之執行個體。 Integration Services Project1 包含此封裝。 本範例呼叫 catalog.set_execution_parameter_value 來設定 Parameter1、Parameter2 和 LOGGING_LEVEL 參數的值。 本範例將呼叫 catalog.start_execution 以啟動執行之執行個體。  
  
```sql
Declare @execution_id bigint  
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Child1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'TestDeply4', @project_name=N'Integration Services Project1', @use32bitruntime=False, @reference_id=Null  
Select @execution_id  
DECLARE @var0 sql_variant = N'Child1.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter1', @parameter_value=@var0  
DECLARE @var1 sql_variant = N'Child2.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter2', @parameter_value=@var1  
DECLARE @var2 smallint = 1  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var2  
EXEC [SSISDB].[catalog].[start_execution] @execution_id  
GO  
```  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   執行執行個體的 READ 和 MODIFY 權限、專案的 READ 和 EXECUTE 權限，以及 (如果適用的話) 參考環境的 READ 權限  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   使用者未具備適當的權限  
  
-   執行識別碼無效  
  
-   執行已啟動或已完成；執行只能啟動一次  
  
-   與專案相關聯的環境參考無效  
  
-   未設定所需的參數值  
  
-   與執行執行個體相關聯的專案版本已過期；只能執行最新版本的專案  
  
  

