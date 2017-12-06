---
title: "將新的或現有的報表新增至報表專案 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: tools
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: reports [Reporting Services], creating
ms.assetid: 8bc0bb53-ad8a-464d-bb6a-7fea5fa62c5c
caps.latest.revision: "20"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: a78b23feb1ca7bcb8cb7ad9ded16c43c8034c395
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="add-a-new-or-existing-report-to-a-report-project-ssrs"></a>將新的或現有的報表加入報表專案 (SSRS)
  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，您可以使用 [報表精靈] 或將新的空白報表加入至專案，藉以加入新的 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表。 您也可以加入現有的報表。 新增報表之後，您就可以看到報表名稱列在專案的 [報表] 資料夾下。  
  
> [!NOTE]  
>  若要預覽具有現有資料來源的報表，您必須擁有報表撰寫用戶端之資料來源的權限。 如需詳細資訊，請參閱 [資料連接、資料來源及連接字串](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)。  
  
 在您加入報表之後，就可以定義資料來源和資料集，以及設計報表配置。 若要開始使用，請參閱[建立基本資料表報表 &#40;SSRS 教學課程&#41;](../../reporting-services/create-a-basic-table-report-ssrs-tutorial.md) 或[資料表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)。  
  
## <a name="to-add-a-new-report-using-the-report-wizard"></a>使用報表精靈來加入新的報表  
  
1.  在方案總管中，以滑鼠右鍵按一下 [報表] 資料夾，然後按一下 [新增新的報表]。 [報表精靈] 對話方塊隨即開啟。  
  
     這個精靈會逐步引導您建立資料來源、建立含有查詢的資料集、定義群組、指定配置以及建立報表。 這些步驟包含：  
  
    -   **選取資料來源。** 建立報表的第一個步驟是定義資料來源。 [報表精靈] 提供報表專案中所有共用資料來源的清單，也提供建立新資料來源的選項。  
  
    -   **設計查詢。** 下一個步驟是設計查詢。 您可以輸入查詢字串、使用查詢設計工具來建立它，或從其他報表匯入查詢。 如需查詢設計工具的相關資訊，請參閱 [Reporting Services 查詢設計工具](http://msdn.microsoft.com/library/07efd3f1-804f-45f7-b62a-3e727a3d9835)。  
  
    -   **選擇報表類型。** 下一個步驟是選取您要的報表類型。 您可以選擇表格式或矩陣報表。 表格式報表有固定的資料行數目。 矩陣 (或稱為交叉資料表) 報表會根據查詢的結果，而有不同的資料行數目。 對應報表會針對地理背景顯示分析。  
  
    -   **為報表命名。**  ：最後一個步驟是為報表命名，並確認報表中將要包含的欄位。 所有步驟都完成之後，報表設計師會建立報表，並將其加入報表伺服器專案。  
  
## <a name="to-add-a-new-blank-report"></a>加入新的空白報表  
  
1.  在 [專案] 功能表中，按一下 [新增項目]。  
  
2.  在 [範本] 中，按一下 [報表]。  
  
3.  按一下 **[加入]**。  
  
     新的空白報表就會加入至專案並且顯示在設計介面上。  
  
## <a name="to-add-an-existing-report"></a>加入現有的報表  
  
1.  在 [專案] 功能表上，按一下 [新增]，然後按一下 [現有項目]。  
  
2.  巡覽至 .rdl 檔的位置、選取該檔案，然後按一下 [新增]。  
  
     報表就會新增至 [報表] 資料夾底下的專案。 當您關閉並重新開啟專案時，這些報表就會按照字母順序排序。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 教學課程 &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
 更多問題嗎？ [試試 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
  
  
