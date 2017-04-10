---
title: "Start the SQL Server Import and Export Wizard | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server 匯入和匯出精靈"
  - "啟動 SQL Server 匯入和匯出精靈"
  - "匯入和匯出精靈"
  - "啟動匯入和匯出精靈"
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
caps.latest.revision: 130
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 112
---
# Start the SQL Server Import and Export Wizard
您可以用下列其中一種方式啟動 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入及匯出精靈]。
-   從 [[開始] 功能表](#startStart)或[命令提示字元](#startCmd)，從任何支援的資料來源匯入或對其匯出。
-   如果您匯入 SQL Server 或從中匯出，可以使用 [SQL Server Management Studio (SSMS)](#startSSMS)。
-   如果您已開啟 SQL Server Integration Services 專案，可以[搭配 SQL Server Data Tools (SSDT) 使用 Visual Studio](#startVS)。

本主題僅描述如何**啟動**精靈。
-   如果您要尋找精靈概觀，請參閱[使用 SQL Server 匯入及匯出精靈匯入和匯出資料](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。
-   如果您要尋找精靈中的步驟相關資訊，請在內容導覽功能表中選取需要的頁面。 精靈每個頁面都有各自的文件。 或在精靈的任何頁面或對話方塊中點選 F1 鍵，以查看目前頁面的文件。

**取得精靈。** 如果您想要執行精靈，但電腦上尚未安裝 [!INCLUDE[msCoName] (../Token/msCoName_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則可以安裝 SQL Server Data Tools (SSDT) 來安裝 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈]。 如需詳細資訊，請參閱[下載 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。  

## <a name="a-namestartstarta-start-the-wizard-from-the-start-menu"></a><a name="startStart"></a>從 [開始] 功能表啟動精靈  
1.  在 [開始] 功能表上，按一下 [所有應用程式]。
2.  找出並展開 [Microsoft SQL Server 2016]。
3.  按一下下列其中一個選項。
  
    -   **SQL Server 2016 匯入和匯出資料 (64 位元)**
          
    -   **SQL Server 2016 匯入和匯出資料 (32 位元)**  
  
除非您確定資料來源需要 32 位元資料提供者，否則請執行 64 位元版本的精靈。
 
![啟動精靈 (開始)](../../integration-services/import-export-data/media/start-wizard-start.jpg)
  
## <a name="a-namestartcmda-start-the-wizard-from-the-command-prompt"></a><a name="startCmd"></a> 從命令提示字元啟動精靈  
在命令提示字元視窗中，執行下列其中一個位置的 **DTSWizard.exe**。  
  
-   **C:\Program Files\Microsoft SQL Server\130\DTS\Binn** (適用於 64 位元版本)。  
  
-   **C:\Program Files (x86)\Microsoft SQL Server\130\DTS\Binn** (適用於 32 位元版本)。  
  
除非您確定資料來源需要 32 位元資料提供者，否則請執行 64 位元版本的精靈。

![啟動精靈 (Cmd)](../../integration-services/import-export-data/media/start-wizard-cmd.jpg)  
  
## <a name="a-namestartssmsa-start-the-wizard-from-sql-server-management-studio-ssms"></a><a name="startSSMS"></a> 從 SQL Server Management Studio (SSMS) 啟動精靈  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體。
2.  展開 **[資料庫]**。
3.  以滑鼠右鍵按一下資料庫。
4.  指向 [工作]。
5.  按一下下列其中一個選項。
  
    -   **匯入資料**
      
    -   **匯出資料**  

![啟動精靈 (SSMS)](../../integration-services/import-export-data/media/start-wizard-ssms.jpg) 

如果您未安裝 SQL Server，或您有 SQL Server 但未安裝 SQL Server Management Studio，請參閱[下載 SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)。
    
## <a name="a-namestartvsa-start-the-wizard-from-visual-studio-with-sql-server-data-tools-ssdt"></a><a name="startVS"></a> 使用 SQL Server Data Tools (SSDT) 從 Visual Studio 啟動精靈  
 在具有 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的 Visual Studio 中開啟 Integration Services 專案，然後執行下列其中一個動作。  
  
-   在 [專案] 功能表上，按一下 [SSIS 匯入和匯出精靈]。 

    ![啟動精靈 (專案)](../../integration-services/import-export-data/media/start-wizard-project.jpg) 
    
    \- 或 -
    
-   在方案總管中，以滑鼠右鍵按一下 [SSIS 封裝] 資料夾，然後按一下 [SSIS 匯入和匯出精靈]。

    ![啟動精靈 (封裝)](../../integration-services/import-export-data/media/start-wizard-packages.jpg)

如果您未安裝 Visual Studio，或您有 Visual Studio 但未安裝 SQL Server Data Tools，請參閱下載 [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。 

## <a name="get-help-while-the-wizard-is-running"></a>在精靈執行時取得說明
> [!TIP] 在精靈的任何頁面或對話方塊中點選 F1 鍵，以查看目前頁面的文件。   

 ## <a name="whats-next"></a>下一步  
 當您啟動精靈時，第一頁是 [歡迎使用 SQL Server 匯入和匯出精靈]。 您不需要在此頁面上採取任何動作。 如需詳細資訊，請參閱[歡迎使用 SQL Server 匯入和匯出精靈](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)。  
  
  