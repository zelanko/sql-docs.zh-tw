---
description: catalog.start_execution (SSISDB 資料庫)
title: catalog.start_execution (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: f8663ff3-aa98-4dd8-b850-b21efada0b87
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f1a69ba2746d688f1d134546370514f826f9cee3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477105"
---
# <a name="catalogstart_execution-ssisdb-database"></a>catalog.start_execution (SSISDB 資料庫)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  啟動在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的執行執行個體。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.start_execution [ @execution_id = ] execution_id [, [ @retry_count = ] retry_count]  
```  
  
## <a name="arguments"></a>引數  
 [@execution_id =] *execution_id*  
 執行之執行個體的唯一識別碼。 *execution_id* 是 **bigint**。
 
 [@retry_count =] *retry_count*  
 執行失敗時的重試次數。 只有當執行位在 Scale Out 中時，它才會生效。這是選擇性參數。 如果未指定，會將其值設定為 0。 *retry_count* 是 **int**。
  
## <a name="remarks"></a>備註  
 已使用執行來指定在套件執行的單一執行個體期間，套件所使用的參數值。 建立執行執行個體之後，在該執行執行個體啟動之前，對應的專案可能已重新部署。 在這種情況下，執行的執行個體將會參考已過期的專案。 無效的參考會導致預存程序失敗。  
  
> [!NOTE]  
>  執行只能啟動一次。 若要啟動執行的執行個體，它必須處於已建立狀態 ([catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) 檢視之 **status** 資料行中的值為 `1`)。  
  
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
 None  
  
## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   執行執行個體的 READ 和 MODIFY 權限、專案的 READ 和 EXECUTE 權限，以及 (如果適用的話) 參考環境的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   使用者未具備適當的權限  
  
-   執行識別碼無效  
  
-   執行已啟動或已完成；執行只能啟動一次  
  
-   與專案相關聯的環境參考無效  
  
-   未設定所需的參數值  
  
-   與執行執行個體相關聯的專案版本已過期；只能執行最新版本的專案  
  
  
