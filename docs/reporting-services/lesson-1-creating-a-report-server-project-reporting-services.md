---
title: 第 1 課：建立報表伺服器專案 (Reporting Services) | Microsoft Docs
ms.date: 05/01/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c3a32b6b27a8919d729c95bfe29f50c2bda81db8
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65095850"
---
# <a name="lesson-1-creating-a-report-server-project-reporting-services"></a>第 1 課：建立報表伺服器專案 (Reporting Services)

在這一課中，您會使用*報表設計師*建立*報表伺服器專案*和*報表定義 (.rdl)* 檔案。

> [!NOTE]
> [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 是 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 環境，可用於建立商務智慧解決方案。 SSDT 的主要功能之一是提供報表設計師的撰寫環境，讓您可以從中開啟、修改、預覽、儲存及部署 [!INCLUDE[ssrsnoversion_md](../includes/ssrsnoversion-md.md)] 編頁報表定義、共用的資料來源、共用資料集與報表組件。

當您使用報表設計師建立報表時，它會建立一個報表伺服器專案，其中包含報表檔案和報表所使用的其他資源檔案。

## <a name="to-create-a-report-server-project"></a>建立報表伺服器專案
  
1. 從 [檔案] 功能表選取 [新增] > [專案]。  

    ![ssrs-ssdt-file-01-new-project](../reporting-services/media/ssrs-ssdt-file-01-new-project.png)
  
2. 在最左邊資料行的 [已安裝] 底下，選取 [Reporting Services]。 在某些情況下，它可能會在 [Business Intelligence] 群組底下。

    ![select-report-server-project-template](../reporting-services/media/lesson-1-creating-a-report-server-project-reporting-services/select-report-server-project-template.png)

    > [!IMPORTANT]
    > 若是 VS，如果您沒有在左側資料行中看到 Reporting Services，則會安裝 SSDT 工作負載來新增報表設計師。 從 [工具] 功能表上，選取 [取得工具與功能...]，然後從顯示的工作負載中選取 [SQL Server Data Tools]。 如果您沒有在中間資料行中看到報表服務物件，請新增 Reporting Services 擴充功能。 從 [工具] 功能表上，選取 [擴充功能和更新] > [線上]。 在中間資料行中，從顯示的擴充功能選取 [Microsoft Reporting Services 專案] > [下載]。 對於 SSDT，請參閱[下載 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)。

3. 在 [新增專案] 對話方塊的中間資料行中，選取 [報表伺服器專案] 圖示&nbsp;&nbsp;![ssrs_ssdt_report_server_project](media/ssrs-ssdt-report-server-project.png) &nbsp;&nbsp;。

4. 在 [名稱] 文字方塊中，輸入 "Tutorial" 作為專案名稱。 根據預設，[位置] 文字方塊會顯示您 "Documents\Visual Studio 20xx\Projects\" 資料夾的路徑。 報表設計師會在此路徑底下建立一個名為 Tutorial 的資料夾，然後在此資料夾中建立 Tutorial 專案。 如果專案不屬於 VS 方案，則 VS 也會建立一個方案檔 (.sln)。

5. 選取 [確定] 可建立專案。 Tutorial 專案會顯示在右邊的 [方案總管] 窗格中。
  
## <a name="creating-a-report-definition-file-rdl"></a>建立報表定義檔案 (RDL)  
  
1. 在 [方案總管] 窗格中，以滑鼠右鍵按一下 [報表] 資料夾。 如果您沒有看到 [方案總管] 窗格，請選取 [檢視] 功能表 > [方案總管]。

2. 選取 [新增] > [新項目]。

    ![ssrs_ssdt_add_report](../reporting-services/media/ssrs-ssdt-add-report.png)

3. 在 [加入新項目] 視窗中，選取 [報表] 圖示。

4. 在 [名稱] 文字方塊中輸入 "Sales Orders.rdl"。

5. 選取 [加入新項目] 對話方塊右下方的 [新增] 按鈕，即可完成此程序。 報表設計師會在 [設計] 檢視中開啟並顯示 Sales Orders 報表檔案。

    ![ssrs-ssdt-01-new-report-designer](media/ssrs-ssdt-01-new-report-designer.png)

## <a name="next-steps"></a>後續步驟

到目前為止，您已經建立了 Tutorial 報表專案和 Sales Orders 報表。 在其餘的課程中，您將了解如何：

- 設定報表的資料來源。
- 從資料來源建立資料集。
- 設計報表版面配置並設定其格式。

請繼續進行[第 2 課：指定連線資訊 &#40;Reporting Services&#41;](../reporting-services/lesson-2-specifying-connection-information-reporting-services.md)。
