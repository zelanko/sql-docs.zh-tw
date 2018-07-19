---
title: 專案屬性頁對話方塊 | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: tools
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- sql13.rpt.rptdesigner.projectpropertypages.general.f1
helpviewer_keywords:
- Project Property Pages dialog box
ms.assetid: 209d9e22-37fc-418f-8739-83adcf447d3f
caps.latest.revision: 35
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: cdec8567dc15962e26b238b90a2b3365f657ac28
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33032480"
---
# <a name="project-property-pages-dialog-box"></a>專案屬性頁對話方塊

  使用專案屬性頁，即可設定報表伺服器專案的部署屬性。 若要開啟此對話方塊，請從 [專案] 功能表按一下 [*\<報表專案名稱>* 屬性]。  
  
 在您定義組態屬性之後，可以從工具列的 [方案組態] 下拉式清單中選取組態。  

![ssrs_project_properties](../../reporting-services/reports/media/ssrs-project-properties.png)
  
## <a name="options"></a>選項。  
 **Configuration**  
 選取要編輯的組態。 一開始會有下列的組態可用： **Debug**、 **DebugLocal**和 **Release**。 使用中組態會先出現，例如 **Active(Debug)**。  
  
 若要同時查看多個組態的屬性，請選取 **[所有組態]** 或 **[多重組態]**。  
  
 若要建立其他組態，請按一下工具列上的 **[組態管理員]** 。  
  
 **[組態管理員]**  
 針對整個方案管理組態或是加入其他組態。 如需詳細資訊，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 文件集。  
  
 **OutputPath**  
 輸入或貼上路徑來儲存報表之建立驗證、部署與預覽時所使用的報表定義。 此路徑必須不同於專案所使用的路徑以及位於專案路徑下之子資料夾的相對路徑。  
  
> [!NOTE]  
>  您可以使用多個組態，以便根據您執行的工作，在路徑之間切換。  
  
 **ErrorLevel**  
 輸入回報為錯誤之建立問題的嚴重性。 嚴重性層級小於或等於 **ErrorLevel** 值的問題會回報為錯誤；否則，會將這些問題回報為警告。 任何錯誤都會導致建立工作失敗。 有效的嚴重性層級為 0 到 4 (包含)。 預設值為 2。  
  
 **StartItem**  
 選取當專案發行到報表伺服器之後，要顯示在網頁瀏覽器中的報表；或當專案在本機執行時，要顯示在預覽視窗中的報表。 建置但不部署專案的設定及 [偵錯] 命令 (**F5**) 的使用都需要開始項目。 部署專案的組態需要它。  
  
 **OverwriteDataSources**  
 選取 **True** ，即可在發行報表時，以專案中的資料來源覆寫伺服器上的資料來源。 選取 **False** ，即可保留伺服器上現有的資料來源。  
  
 **TargetServerVersion**  
 選取 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，或選取 [偵測版本] 自動判斷安裝在 **TargetServer URL** 屬性所識別之伺服器上的版本。 預設值是 **SQL Server 2016**。  
  
 **TargetDataSourceFolder**  
 用來儲存已發行共用資料來源的資料夾名稱。 如果您未指定資料夾，資料來源就會發行到與報表相同的資料夾。 如果報表伺服器上沒有此資料夾，報表設計師會在發行報表時建立資料夾。  
  
 發行至以原生模式執行的報表伺服器時，請從根目錄開始指定資料夾階層的完整路徑。 例如，Folder1/Folder2/Folder3。  
  
 發行至以 SharePoint 整合模式執行的報表伺服器時，請使用 SharePoint 文件庫的 URL。 例如， `http:\\<servername>\<site>\Documents\MyFolder`。  
  
 **TargetReportFolder**  
 用來儲存已發行報表的資料夾名稱。 依預設，此為報表專案的名稱。 如果報表伺服器上沒有此資料夾，報表設計師會在發行報表時建立資料夾。  
  
 發行至以原生模式執行的報表伺服器時，請從根目錄開始指定資料夾階層的完整路徑。 如果某個資料夾位於另一個資料夾內，請從根目錄開始加入資料夾的路徑，例如 Folder1/Folder2/Folder3。  
  
 發行至以 SharePoint 整合模式執行的報表伺服器時，請使用 SharePoint 文件庫的 URL。 例如， `http:\\<servername>\\<site>\Documents\MyFolder`。  
  
 **TargetServerURL**  
 目標報表伺服器的 URL。 在發行報表之前，您必須設定此屬性為有效的報表伺服器 URL。  
  
 發行到以原生模式執行的報表伺服器時，請使用報表伺服器虛擬目錄的 URL。 例如， `http:\\<server>\reportserver`。 這是報表伺服器的虛擬目錄，而非報表管理員。 依預設，報表伺服器會安裝在名稱為 [reportserver] 的虛擬目錄中。  
  
 發行至以 SharePoint 整合模式執行的報表伺服器時，請使用 SharePoint 頂層網站或子網站的 URL。 若未指定網站，則會使用預設的最上層網站。 例如： 
+ `http:\\<servername>`、 
+ `http:\\<servername\<site>` 
+ `http:\\<servername>\<site>\<subsite>`。  

## <a name="next-steps"></a>後續步驟

[發行報表](http://msdn.microsoft.com/library/ef5a514e-e818-4041-a8b0-15835f9a046b)   
[將報表發行到 SharePoint 文件庫](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
[設定部署屬性 &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
[報表設計師 F1 說明](../../reporting-services/tools/report-designer-f1-help.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
