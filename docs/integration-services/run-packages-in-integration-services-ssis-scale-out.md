---
title: "執行 Integration Services (SSIS) 相應放大的套件 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4c2f4cd7-9c47-416d-bb1e-40acc3e05342
caps.latest.revision: 5
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 5
---
# 執行 Integration Services (SSIS) 相應放大的套件
在封裝部署到 Integration Services 伺服器之後，您可以在相應放大中執行它們。

## <a name="run-packages-with-execute-package-in-scale-out-dialog"></a>執行具有 [在相應放大中執行套件] 對話方塊的套件 

1. ### <a name="open-the-execute-package-in-scale-out-dialog-box"></a>開啟 [在相應放大中執行套件] 對話方塊 ###
    在 [!INCLUDE[ssManStudioFull_md](../includes/ssmanstudiofull-md.md)] 中連接到 Integration Services 伺服器。 在 [物件總管] 中，展開樹狀目錄以顯示 [Integration Services 目錄] 下的節點。 以滑鼠右鍵按一下 [SSISDB] 節點或您要執行的專案或封裝，再按一下 [在相應放大中執行]。
2. ### <a name="select-packages-and-set-the-options"></a>選取封裝並設定選項 ###
    在 [選取套件] 頁面上，選取多個要執行的封裝，並設定環境、參數、連接管理員以及每個封裝的進階選項。 按一下封裝設定這些選項。
    
    在 [進階] 索引標籤上，設定稱為 [重試計數] 的相應放大選項。 它會設定封裝執行失敗時重試的次數。
3. ### <a name="select-machines"></a>選取電腦 ###
    在 [選取電腦] 頁面上，選取相應放大背景工作電腦來執行封裝。 依預設，任何電腦皆可執行套件。 

   > [!NOTE]
> [選取電腦] 頁面會顯示使用相應放大背景工作服務的使用者帳戶認證執行的封裝。 預設的帳戶是 NT Service\SSISScaleOutWorker140。 您可能會想要變更為自己的實驗室帳戶。

4. ### <a name="run-the-packages-and-view-reports"></a>執行套件並檢視報表 
    按一下 [確定] 開始執行封裝。 若要檢視封裝的執行報表，請以滑鼠右鍵按一下 [物件總管] 中的封裝，再依序按一下 [報表] 及 [所有執行]，找到執行。
    
    
## <a name="run-packages-with-stored-procedures"></a>以預存程序執行套件

1. ### <a name="create-executions"></a>建立執行 ###
    呼叫每個封裝的 [catalog].[create_execution]。 將參數 **@runincluster** 設為 True。 如果不是所有的相應放大背景工作電腦都可以執行套件，請將參數 **@useanyworker** 設為 False。   
2. ### <a name="set-execution-parameters"></a>設定執行參數 ###
    呼叫每個執行的 [catalog].[set_execution_parameter_value]。
3. ### <a name="set-scale-out-workers"></a>設定相應放大背景工作 ###
    呼叫 [catalog].[add_execution_worker]。 如果所有的電腦都可以執行套件，即不必呼叫此預存程序。 
4. ### <a name="start-executions"></a>啟動執行 ###
    呼叫 [catalog].[start_execution]。 設定參數 **@retry_count** 以設定封裝執行失敗時重試的次數。
    
    ### <a name="example"></a>範例  ###  
    下例會使用一個相應放大背景工作在相應放大中執行兩個套件：package1.dtsx 和 package2.dtsx。  
    ```
    Declare @execution_id bigint
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder1', @project_name=N'project1', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runincluster=True
    Select @execution_id
    DECLARE @var0 smallint = 1
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
    EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
    EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
    GO

    Declare @execution_id bigint
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package2.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder2', @project_name=N'project2', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runincluster=True
    Select @execution_id
    DECLARE @var0 smallint = 1
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
    EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
    EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
    GO
    ```


## <a name="permissions"></a>Permissions
在相應放大中執行套件需要下列權限之一︰

-   **ssis_admin** 資料庫角色中的成員資格  

-   **ssis_cluster_executor** 資料庫角色中的成員資格  
  
-   **sysadmin** 伺服器角色中的成員資格  
    