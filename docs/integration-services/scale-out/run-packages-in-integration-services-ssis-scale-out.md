---
title: 執行 SQL Server Integration Services (SSIS) Scale Out 中的套件 | Microsoft Docs
description: 本文描述如何在 Scale Out 中執行 SSIS 套件
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.reviewer: maghan
f1_keywords:
- sql13.ssis.ssms.ispackageexecuteinscaleout.f1
ms.openlocfilehash: c2457b1425e8c769439f62ddae3848c82ec1b4aa
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763219"
---
# <a name="run-packages-in-integration-services-ssis-scale-out"></a>執行 Integration Services (SSIS) Scale Out 中的套件

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


將套件部署至 Integration Services 伺服器之後，即可使用下列其中一種方法在 Scale Out 中予以執行：

-   [在擴增中執行套件對話方塊](#scale_out_dialog)

-   [預存程序](#stored_proc)

-   [SQL Server Agent 作業](#sql_agent)

## <a name="run-packages-with-the-execute-package-in-scale-out-dialog-box"></a><a name="scale_out_dialog"></a> 使用 [在擴增中執行套件] 對話方塊執行套件

1. 開啟 [在擴增中執行套件] 對話方塊。

    在 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)]中連接到 Integration Services 伺服器。 在 [物件總管] 中，展開樹狀目錄以顯示 [Integration Services 目錄]  下的節點。 以滑鼠右鍵按一下 [SSISDB]  節點或您要執行的專案或封裝，再按一下 [在擴增中執行]  。

2. 選取套件，並設定選項。

    在 [選取套件]  頁面上，選取要執行的一或多個套件。 設定每個套件的環境、參數、連線管理員和進階選項。 按一下封裝設定這些選項。
    
    在 [進階]  索引標籤上，設定稱為 [重試計數]  的 Scale Out 選項來指定套件執行失敗時的重試次數。

    > [!NOTE]
    > 只有在執行 Scale Out Worker 服務的帳戶是本機電腦的系統管理員時，[在發生錯誤時傾印]  選項才會作用。

3. 選取背景工作電腦。

    在 [選取電腦]  頁面上，選取 Scale Out Worker 電腦來執行套件。 根據預設，任何電腦皆可執行套件。 

   > [!NOTE] 
   > 套件是使用 Scale Out Worker 服務的使用者帳戶認證所執行。 檢閱 [選取電腦]  頁面上的這些認證。 帳戶預設為 `NT Service\SSISScaleOutWorker140`。

   > [!WARNING]
   > 相同背景工作上不同使用者所觸發的套件執行，都是使用相同的認證來執行。 它們之間沒有安全性界限。 

4. 執行套件，並檢視報表。

    按一下 [確定]  開始執行封裝。 若要檢視封裝的執行報表，請以滑鼠右鍵按一下 [物件總管] 中的封裝，再依序按一下 [報表]  及 [所有執行]  ，找到執行。
    
## <a name="run-packages-with-stored-procedures"></a><a name="stored_proc"></a> 以預存程序執行套件

1.  建立執行。

    針對每個套件，呼叫 `[catalog].[create_execution]`。 將參數 **\@runinscaleout** 設為 `True`。 如果並非所有 Scale Out Worker 電腦都可以執行套件，則請將參數 **\@useanyworker** 設為 `False`。 如需此預存程序和 **\@useanyworker** 參數的詳細資訊，請參閱 [catalog.create_execution](../system-stored-procedures/catalog-create-execution-ssisdb-database.md)。 

2. 設定執行參數。

    針對每次執行，呼叫 `[catalog].[set_execution_parameter_value]`。

3. 設定 Scale Out Worker。

    呼叫 `[catalog].[add_execution_worker]`。 如果所有電腦都可以執行套件，就不需要呼叫此預存程序。 

4. 開始執行。

    呼叫 `[catalog].[start_execution]`。 設定參數 **\@retry_count**，以設定套件執行失敗時的重試次數。
    
### <a name="example"></a>範例
下列範例會使用一個 Scale Out Worker 在 Scale Out 中執行兩個套件：`package1.dtsx` 和 `package2.dtsx`。  

```sql
Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder1', @project_name=N'project1', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runinscaleout=True
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
GO

Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package2.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder2', @project_name=N'project2', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runinscaleout=True
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
GO
```

### <a name="permissions"></a>權限
若要在 Scale Out 中執行套件，您需要具有下列其中一種權限︰

-   **ssis_admin** 資料庫角色中的成員資格  

-   **ssis_cluster_executor** 資料庫角色中的成員資格  
  
-   **sysadmin** 伺服器角色中的成員資格  

## <a name="set-default-execution-mode"></a>設定預設執行模式
若要將套件的預設執行模式設定為 [擴增]  ，請執行下列動作：

1.  在 SSMS 的物件總管中，以滑鼠右鍵按一下 [SSISDB]  節點，然後選取 [屬性]  。

2.  在 [目錄屬性]  對話方塊中，將 [全伺服器的預設執行模式]  設定為 [擴增]  。

設定這個預設執行模式之後，在呼叫 `[catalog].[create_execution]` 預存程序時，就不再需要指定 **\@runinscaleout** 參數。 套件會自動以擴增模式執行。 

![執行模式](media/exe-mode.PNG)

若要重新切換預設執行模式，讓套件不再預設以擴增模式執行，請將 [全伺服器的預設執行模式]  設定為 [伺服器]  。

## <a name="run-package-in-sql-server-agent-job"></a><a name="sql_agent"></a> 在 SQL Server Agent 作業中執行套件
在 SQL Server Agent 作業中，您可以將 SSIS 套件執行為作業的一個步驟。 若要以擴增執行套件，請將預設執行模式設定為 [擴增]  。將預設執行模式設定為 [擴增]  之後，即會以擴增模式執行 SQL Server Agent 作業中的套件。

## <a name="next-steps"></a>後續步驟
-   [為擴增進行疑難排解](troubleshooting-scale-out.md)
