---
title: "將 BI 語意模型連接內容類型加入至程式庫 |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 145505ed-50bc-4528-912b-2a5cd2566011
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4438608a9e2b5ed5e4e642afa239186db863f578
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="add-bi-semantic-model-connection-content-type-to-library"></a>將 BI 語意模型連接內容類型加入至程式庫
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
BI 語意模型連接是在 SharePoint 中所建立，它會重新導向至網路伺服器上 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿或 Analysis Services 表格式模型資料庫內的商業智慧語意模型資料。 在 SharePoint 中建立 BI 語意模型連接之前，您必須擴充文件庫以允許建立 .bism 檔。 針對每個文件庫，僅需要執行一次這個步驟，但是您將需要針對您要建立 .bism 檔的任何來源文件庫重複該步驟。 最佳做法建議您建立集中式文件庫來儲存 .bism 檔，讓您可以在一個地方管理權限。  
  
> [!NOTE]  
>  如果您已經使用 SharePoint 資料連線庫，則會將 BI 語意模型連接內容類型自動加入至該連線庫範本。 如果您使用已經讓您建立新 BI 語意模型連接文件的資料連線庫，可以略過本節中的步驟。  
  
##  <a name="bkmk_addtype"></a> 將內容類型加入至文件庫  
 您必須至少有「管理清單」權限，才能加入並設定內容類型。 此權限內建在「設計」權限等級以上 (含)。  
  
 包含文件庫的網站必須啟用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的功能。 如需詳細資訊，請參閱 [在管理中心為網站集合啟用 Power Pivot 功能整合](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md)。  
  
1.  開啟要啟用 BI 語意模型連接內容類型的文件庫。  
  
2.  在 SharePoint 功能區的 [文件庫工具] 中，按一下 **[文件庫]**。  
  
3.  按一下 **[文件庫設定]**。  
  
4.  按一下 [一般設定] 中的 **[進階設定]**。  
  
5.  在 [內容類型] 的 [是否允許內容類型的管理?] 區段中按一下 **[是]**。  
  
6.  按一下 **[確定]**。  
  
7.  在 [內容類型] 區段中，按一下 **[從現有的網站內容類型新增]**。 如果您看不到此頁面，請回到網站中，按一下文件庫工具中的 **[文件庫]** ，然後按一下 **[文件庫設定]**。  
  
8.  在 [內容類型] 中，按一下 **[從現有的網站內容類型新增]**。  
  
9. 在 [從下列位置選取網站內容類型:] 中，選取 **[商業智慧]**。  
  
10. 在 [可用的網站內容類型] 中，按一下 **[BI 語意模型連接檔案]**，然後按一下 **[加入]** ，將所選取的內容類型移到 [要新增的內容類型] 清單中。  
  
11. 按一下 **[確定]**。  
  
12. 若要驗證您是否加入此內容類型，請回到文件庫，然後在文件庫功能區的文件區域上按一下 **[新文件]** 。 您應該會在 [新文件] 清單中看到 **[BI 語意模型連接檔案]** 。  
  
     ![在 SharePoint 文件庫中的新文件子功能表](../../analysis-services/power-pivot-sharepoint/media/ssas-bismconnection-new.gif "SharePoint 文件庫中的新文件子功能表")  
  
 在您為文件庫啟用 BI 語意模型連接內容類型之後，您可以建立連接來重新導向至可由 Excel 或 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 報表使用的商業語意模型資料。 從下列連結進行選擇，以深入了解下一個步驟：  
  
 [建立與 Power Pivot 活頁簿的 BI 語意模型連接](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
 [建立與表格式模型資料庫的 BI 語意模型連接](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)  
  
## <a name="see-also"></a>另請參閱  
 [Power Pivot BI 語意模型連接 &#40;.bism&#41;](../../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [使用 Excel 或 Reporting Services 中的 BI 語意模型連接](../../analysis-services/power-pivot-sharepoint/use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)  
  
  
