---
title: "第 1 課： 建立報表伺服器專案 (Reporting Services) |Microsoft 文件"
ms.custom: 
ms.date: 11/30/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
caps.latest.revision: 57
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: bead48dd2f32047b2782a54204bf06a145a7d71d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-1-creating-a-report-server-project-reporting-services"></a>第 1 課：建立報表伺服器專案 (Reporting Services)

 > 如需舊版的 SQL Server 相關的內容，請參閱[第 1 課： 建立報表伺服器專案 (Reporting Services)](https://msdn.microsoft.com/en-US/library/ms167559(SQL.120).aspx)。

在這一課中，您將會在 Visual Studio 中以 *建立「報表伺服器專案」**和「報表定義 (.rdl)」*[!INCLUDE[ssBIDevStudio_md](../includes/ssbidevstudio-md.md)] 檔案。 

若要使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]建立報表，首先您需要報表伺服器專案，您可在其中儲存報表定義 (.rdl) 檔案以及報表所需的任何其他資源檔案。 

在後續課程中，您將定義報表的資料來源、定義資料集，以及定義報表配置。 當您執行報表時，會擷取資料並與版面配置結合，然後轉譯顯示於螢幕上。 您之後可以將報表匯出、列印或儲存。  
  
  
  
## <a name="to-create-a-report-server-project"></a>建立報表伺服器專案  
  
1.  開啟 [!INCLUDE[ssBIDevStudio_md](../includes/ssbidevstudio-md.md)]。  
  
2.  在**檔案**功能表 >**新增** > **專案**。  

    ![ssrs-ssdt-file-01-new-project](../reporting-services/media/ssrs-ssdt-file-01-new-project.png)
  
3.  在下**已安裝** > **範本** > **Business Intelligence**，按一下  **Reporting Services**。

    ![ssrs-ssdt-01-new-rs-project](../reporting-services/media/ssrs-ssdt-01-new-rs-project.png)

5. 按一下 [報表伺服器專案]  ![ssrs_ssdt_report_server_project](../reporting-services/media/ssrs-ssdt-report-server-project.png)。 

   >**請注意**： 如果您沒有看到**Business Intelligence**或**報表伺服器專案**選項，您必須使用來更新 SSDT 商業智慧範本。 請參閱 [下載 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)  
  
5.  在 [名稱] 中，輸入 **Tutorial**。  

    根據預設，會建立在 Visual Studio 2015\Projects 資料夾內的新目錄中。
    
    ![ssrs-ssdt-01-solution-location](../reporting-services/media/ssrs-ssdt-01-solution-location.png)
  
6.  按一下 **[確定]** 建立專案。  
  
    Tutorial 專案會顯示在右邊的 [方案總管] 窗格中。  
  
## <a name="to-create-a-new-report-definition-file"></a>建立新的報表定義檔案  
  
1.  在**方案總管 中** 窗格中，以滑鼠右鍵按一下**報表** > **新增** > **新項目**。 

    >**秘訣**：如果您沒有看到 [方案總管]  窗格，請在 [檢視]  功能表上按一下 [方案總管] 。 

    ![ssrs_ssdt_add_report](../reporting-services/media/ssrs-ssdt-add-report.png)
  
2.  在 [新增項目]  視窗中，按一下 [報表]  ![ssrs_ssdt_report](../reporting-services/media/ssrs-ssdt-report.png)。  
  
3.  在 [名稱] 中，輸入 **Sales Orders.rdl** ，然後按一下 [新增] 。  
  
    報表設計師會在 [設計] 檢視中開啟並顯示新的 .rdl 檔案。  
    
    ![ssrs-ssdt-01-new-report-designer](../reporting-services/media/ssrs-ssdt-01-new-report-designer.png)
  
     報表設計師是一個在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中執行的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]元件。 它有兩個檢視：[設計]  和 [預覽] 。 按一下各個索引標籤，即可變更檢視。  
  
    您會在 [報表資料]  窗格中定義資料， 並在 [設計]  檢視中定義報表配置。 您可以執行報表，然後在 [預覽]  檢視中查看外觀。  
  
## <a name="next-lesson"></a>下一課  
您已順利建立稱為 "Tutorial" 的報表專案，並將報表定義 (.rdl) 檔案加入至報表專案。 下一步，您將指定報表要用的資料來源。 請參閱[第 2 課： 指定連接資訊 &#40;Reporting Services &#41;](../reporting-services/lesson-2-specifying-connection-information-reporting-services.md).  
  
## <a name="see-also"></a>另請參閱  
[建立基本資料表報表 &#40;SSRS 教學課程&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  


