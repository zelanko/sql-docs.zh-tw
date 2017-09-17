---
title: "SQL Server Integration Services (SSIS) 中的執行的封裝向外延展 |Microsoft 文件"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
f1_keywords:
- sql13.ssis.ssms.ispackageexecuteinscaleout.f1
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2c158ae6a711ecb5f5065561c0c8c303e9a09980
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---

# <a name="run-packages-in-integration-services-ssis-scale-out"></a>在 Integration Services (SSIS) 向外執行封裝
在封裝部署到 Integration Services 伺服器之後，您可以在相應放大中執行它們。

## <a name="run-packages-with-execute-package-in-scale-out-dialog"></a>封裝執行執行封裝中向外對話方塊 

1. 開啟 [在相應放大中執行套件] 對話方塊

    在 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 中連接到 Integration Services 伺服器。 在 [物件總管] 中，展開樹狀目錄以顯示 [Integration Services 目錄] 下的節點。 以滑鼠右鍵按一下 [SSISDB]  節點或您要執行的專案或封裝，再按一下 [在相應放大中執行] 。

2. 選取封裝並設定選項

    在 [選取套件]  頁面上，選取多個要執行的封裝，並設定環境、參數、連接管理員以及每個封裝的進階選項。 按一下封裝設定這些選項。
    
    在 [進階]  索引標籤上，設定稱為 [重試計數] 的相應放大選項。 它會設定封裝執行失敗時重試的次數。

    > [!Note]
    > **在錯誤時傾印**選項才會生效，當執行標尺出 Worker 服務的帳戶是本機電腦的系統管理員。

3. 選取電腦

    在 [選取電腦]  頁面上，選取相應放大背景工作電腦來執行封裝。 依預設，任何電腦皆可執行套件。 

   > [!Note] 
   > [選取電腦]  頁面會顯示使用相應放大背景工作服務的使用者帳戶認證執行的封裝。 預設的帳戶是 NT Service\SSISScaleOutWorker140。 您可能會想要變更為自己的實驗室帳戶。

   >[!WARNING]
   >在相同的背景工作上的不同使用者所觸發的封裝執行會以相同的帳戶執行。 在它們之間沒有安全性界限。 

4. 執行套件並檢視報表 

    按一下 [確定]  開始執行封裝。 若要檢視封裝的執行報表，請以滑鼠右鍵按一下 [物件總管] 中的封裝，再依序按一下 [報表] 及 [所有執行] ，找到執行。
    
## <a name="run-packages-with-stored-procedures"></a>以預存程序執行套件

1. 建立執行

    呼叫每個封裝的 [catalog].[create_execution]。 將參數 **@runinscaleout** 設為 True。 如果不是所有的相應放大背景工作電腦都可以執行套件，請將參數 **@useanyworker** 設為 False。   

2. 設定執行參數

    呼叫每個執行的 [catalog].[set_execution_parameter_value]。

3. 設定相應放大背景工作

    呼叫 [catalog].[add_execution_worker]。 如果所有的電腦都可以執行套件，即不必呼叫此預存程序。 

4. 啟動執行

    呼叫 [catalog].[start_execution]。 設定參數 **@retry_count** 以設定封裝執行失敗時重試的次數。
    
#### <a name="example"></a>範例
下例會使用一個相應放大背景工作在相應放大中執行兩個套件：package1.dtsx 和 package2.dtsx。  

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

### <a name="permissions"></a>Permissions
在相應放大中執行套件需要下列權限之一︰

-   **ssis_admin** 資料庫角色中的成員資格  

-   **ssis_cluster_executor** 資料庫角色中的成員資格  
  
-   **sysadmin** 伺服器角色中的成員資格  

## <a name="set-default-execution-mode"></a>設定預設的執行模式
若要設定預設的執行模式以 「 小數位數出 」，以滑鼠右鍵按一下**SSISDB**節點在物件總管 中的 SSMS，並選取**屬性**。
在**目錄屬性**對話方塊中，設定**全伺服器的預設執行模式**至**向外**。

此設定之後, 就不需要指定 **@runinscaleout** 參數 [catalog]。 [create_execution]。 執行會在向外自動執行。 

![Exe 模式](media\exe-mode.PNG)

若要切換回非-小數位數 Out 模式的預設的執行模式，只要將**全伺服器的預設執行模式**至**伺服器**。

## <a name="run-package-in-sql-agent-job"></a>SQL agent 作業中執行封裝
在 Sql 代理程式工作中，您可以選擇執行 SSIS 封裝當做工作的一個步驟。 若要在向外執行封裝，您可以利用上述預設執行模式。 之後設定以 「 小數位數出 」 的預設執行模式下，Sql agent 作業中的封裝會在向外執行。
