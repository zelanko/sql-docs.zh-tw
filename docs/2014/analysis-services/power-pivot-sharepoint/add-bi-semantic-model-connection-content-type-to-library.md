---
title: 將 BI 語意模型連接內容類型新增至程式庫 (PowerPivot for SharePoint) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 145505ed-50bc-4528-912b-2a5cd2566011
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 15537b159f34df3e69c3b415a8a00845ff2fe79f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37284104"
---
# <a name="add-a-bi-semantic-model-connection-content-type-to-a-library-powerpivot-for-sharepoint"></a>將 BI 語意模型連接內容類型加入至文件庫 (PowerPivot for SharePoint)
  BI 語意模型連接是在 SharePoint 中所建立，它會重新導向至網路伺服器上 PowerPivot 活頁簿或 Analysis Services 表格式模型資料庫內的商業智慧語意模型資料。 在 SharePoint 中建立 BI 語意模型連接之前，您必須擴充文件庫以允許建立 .bism 檔。 針對每個文件庫，僅需要執行一次這個步驟，但是您將需要針對您要建立 .bism 檔的任何來源文件庫重複該步驟。 最佳做法建議您建立集中式文件庫來儲存 .bism 檔，讓您可以在一個地方管理權限。  
  
> [!NOTE]  
>  如果您已經使用 SharePoint 資料連線庫，則會將 BI 語意模型連接內容類型自動加入至該連線庫範本。 如果您使用已經讓您建立新 BI 語意模型連接文件的資料連線庫，可以略過本節中的步驟。  
  
##  <a name="bkmk_addtype"></a> 將內容類型加入至文件庫  
 您必須至少有「管理清單」權限，才能加入並設定內容類型。 此權限內建在「設計」權限等級以上 (含)。  
  
 包含文件庫的網站必須啟用 PowerPivot for SharePoint 的功能。 如需詳細資訊，請參閱 <<c0> [ 在管理中心為網站集合啟用 PowerPivot 功能整合](activate-power-pivot-integration-for-site-collections-in-ca.md)。  
  
1.  開啟要啟用 BI 語意模型連接內容類型的文件庫。  
  
2.  在 SharePoint 功能區的 [文件庫工具] 中，按一下 **[文件庫]**。  
  
3.  按一下 **[文件庫設定]**。  
  
4.  按一下 [一般設定] 中的 **[進階設定]**。  
  
5.  在 [內容類型] 的 [是否允許內容類型的管理?] 區段中按一下 **[是]**。  
  
6.  按一下 [確定] 。  
  
7.  在 [內容類型] 區段中，按一下 **[從現有的網站內容類型新增]**。 如果您看不到此頁面，請回到網站中，按一下文件庫工具中的 **[文件庫]** ，然後按一下 **[文件庫設定]**。  
  
8.  在 [內容類型] 中，按一下 **[從現有的網站內容類型新增]**。  
  
9. 在 [從下列位置選取網站內容類型:] 中，選取 **[商業智慧]**。  
  
10. 在 [可用的網站內容類型] 中，按一下 **[BI 語意模型連接檔案]**，然後按一下 **[加入]** ，將所選取的內容類型移到 [要新增的內容類型] 清單中。  
  
11. 按一下 [確定] 。  
  
12. 若要驗證您是否加入此內容類型，請回到文件庫，然後在文件庫功能區的文件區域上按一下 **[新文件]** 。 您應該會在 [新文件] 清單中看到 **[BI 語意模型連接檔案]** 。  
  
     ![在 SharePoint 文件庫中的新文件子功能表](../media/ssas-bismconnection-new.gif "SharePoint 文件庫中的新文件子功能表")  
  
 在您為文件庫啟用 BI 語意模型連接內容類型之後，您可以建立連接來重新導向至可由 Excel 或 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 報表使用的商業語意模型資料。 從下列連結進行選擇，以深入了解下一個步驟：  
  
 [建立與 PowerPivot 活頁簿的 BI 語意模型連接](create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
 [C建立與表格式模型資料庫的 BI 語意模型連接](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)  
  
## <a name="see-also"></a>另請參閱  
 [PowerPivot BI 語意模型連接&#40;.bism&#41;](power-pivot-bi-semantic-model-connection-bism.md)   
 [在 Excel 或 Reporting Services 使用 BI 語意模型連接](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)  
  
  
