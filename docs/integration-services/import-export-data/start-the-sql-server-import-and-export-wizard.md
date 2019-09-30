---
title: 啟動 SQL Server 匯入和匯出精靈 | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Import and Export Wizard
- starting SQL Server Import and Export Wizard
- Import and Export Wizard
- starting Import and Export Wizard
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d54a4d4363b2585d951ca0621306427f8f0e8533
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285117"
---
# <a name="start-the-sql-server-import-and-export-wizard"></a>啟動 SQL Server 匯入和匯出精靈

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]




使用本主題中所述的其中一種方式來啟動 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈]，以從中匯入資料，並將資料匯出至任何支援的資料來源。

> [!IMPORTANT]
> 本主題僅描述如何 **啟動** 精靈。 如需其他資訊，請參閱[相關的工作及內容](#related)。

您可以啟動精靈：
-   從 [[開始] 功能表](#startStart)。
-   從 [命令提示字元](#startCmd)。 
-   如果您匯入 SQL Server 或從中匯出，可以使用 [SQL Server Management Studio (SSMS)](#startSSMS)。
-   如果您匯入 SQL Server 或從中匯出，可以使用 [搭配 SQL Server Data Tools (SSDT) 使用 Visual Studio](#startVS)。

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>必要條件 - 電腦上已安裝精靈嗎？
如果您想要執行精靈，但電腦上尚未安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則可以安裝 SQL Server Data Tools (SSDT) 來安裝 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈]。 如需詳細資訊，請參閱 [下載 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。

> [!NOTE]
> 若要使用 64 位元版本的 [SQL Server 匯入和匯出精靈]，您必須安裝 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位元應用程式，而且只會安裝 32 位元檔案 (包含 32 位元版本的精靈)。

## <a name="startStart"></a> [開始] 功能表  
### <a name="start-the-sql-server-import-and-export-wizard-from-the-start-menu"></a>從開始功能表中啟動 SQL Server 匯入和匯出精靈
1.  在 [開始]  功能表上，找出並展開 [Microsoft SQL Server 2016]  。
3.  按一下下列其中一個選項。
  
    -   **SQL Server 2016 匯入和匯出資料 (64 位元)**
          
    -   **SQL Server 2016 匯入和匯出資料 (32 位元)**  
  
    除非您確定資料來源需要 32 位元資料提供者，否則請執行 64 位元版本的精靈。
 
    ![啟動精靈 (開始)](../../integration-services/import-export-data/media/start-wizard-start.jpg)
  
## <a name="startCmd"></a> Command prompt
### <a name="start-the-sql-server-import-and-export-wizard-from-the-command-prompt"></a>從命令提示字元中啟動 SQL Server 匯入和匯出精靈  
在命令提示字元視窗中，執行下列其中一個位置的 **DTSWizard.exe** 。  
  
-   **C:\Program Files\Microsoft SQL Server\130\DTS\Binn** (適用於 64 位元版本)。  
  
-   **C:\Program Files (x86)\Microsoft SQL Server\130\DTS\Binn** (適用於 32 位元版本)。  
  
除非您確定資料來源需要 32 位元資料提供者，否則請執行 64 位元版本的精靈。

![啟動精靈 (Cmd)](../../integration-services/import-export-data/media/start-wizard-cmd.jpg)  
  
## <a name="startSSMS"></a> SQL Server Management Studio (SSMS)
### <a name="start-the-sql-server-import-and-export-wizard-from-sql-server-management-studio-ssms"></a>從 SQL Server Management Studio (SSMS) 啟動 SQL Server 匯入和匯出精靈    
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。
    
2.  展開 **[資料庫]** 。
3.  以滑鼠右鍵按一下資料庫。
4.  指向 [工作]  。
5.  按一下下列其中一個選項。
  
    -   **匯入資料**
      
    -   **匯出資料**  

    ![啟動精靈 (SSMS)](../../integration-services/import-export-data/media/start-wizard-ssms.jpg) 

如果您未安裝 SQL Server，或您有 SQL Server 但未安裝 SQL Server Management Studio，請參閱 [下載 SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)。
  
## <a name="startVS"></a> Visual Studio
### <a name="start-the-sql-server-import-and-export-wizard-from-visual-studio-with-sql-server-data-tools-ssdt"></a>使用 SQL Server Data Tools (SSDT) 從 Visual Studio 啟動 SQL Server 匯入和匯出精靈 
 在具有 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的 Visual Studio 中開啟 Integration Services 專案，然後執行下列其中一個動作。 
  
-   在 [專案]  功能表上，按一下 [SSIS 匯入和匯出精靈]  。 

    ![啟動精靈 (專案)](../../integration-services/import-export-data/media/start-wizard-project.jpg) 
    
    \- 或 -
    
-   在方案總管中，以滑鼠右鍵按一下 [SSIS 封裝]  資料夾，然後按一下 [SSIS 匯入和匯出精靈]  。

    ![啟動精靈 (封裝)](../../integration-services/import-export-data/media/start-wizard-packages.jpg)

如果您未安裝 Visual Studio，或您有 Visual Studio 但未安裝 SQL Server Data Tools，請參閱下載 [SQL Server Data Tools (SSDT)](../../ssdt/download-sql-server-data-tools-ssdt.md)。

## <a name="get-the-wizard"></a>取得精靈
如果您想要執行精靈，但電腦上尚未安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則可以安裝 SQL Server Data Tools (SSDT) 來安裝 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈]。 如需詳細資訊，請參閱 [下載 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。

## <a name="get-help-while-the-wizard-is-running"></a>在精靈執行時取得說明
> [!TIP]
> 在精靈的任何頁面或對話方塊中點選 F1 鍵，以查看目前頁面的文件。   

 ## <a name="whats-next"></a>下一步  
 當您啟動精靈時，第一頁是 [歡迎使用 SQL Server 匯入和匯出精靈]  。 您不需要在此頁面上採取任何動作。 如需詳細資訊，請參閱 [歡迎使用 SQL Server 匯入和匯出精靈](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)。  
  
## <a name="related"></a> 相關的工作及內容  
 以下是一些其他基本工作。
-   **請參閱精靈運作方式的簡單範例**。

    -   **若要檢視螢幕擷取畫面。** 您可以參考單一頁面上顯示的簡單端對端範例，[從 [匯入及匯出精靈] 的簡單範例開始著手](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)。

    -   **若要觀看影片。** YouTube 上備有此精靈的示範影片，片長四分鐘。影片中將專門針對如何[使用 SQL Server 的 [匯入及匯出精靈]，將資料匯出至 Excel ](https://go.microsoft.com/fwlink/?linkid=829049)清楚地說明。

-   **深入了解此精靈的運作方式。**

    -   **深入了解此精靈。** 如果您要尋找精靈概觀，請參閱 [使用 SQL Server 匯入及匯出精靈匯入和匯出資料](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。

    -   **了解此精靈的步驟。** 如需此精靈之各項步驟的資訊，請參閱 [SQL Server 匯入及匯出精靈的步驟](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)。 文件中另有專頁會列出此精靈的每一個頁面。

    -   **了解如何連線至資料來源和目的地。** 如果您要尋找如何連線至資料的資訊，請從這裡的清單中選取您想要的頁面 - [使用 SQL Server 匯入和匯出精靈連線至資料來源](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)。 數個常用資料來源都各有個別文件頁面。


