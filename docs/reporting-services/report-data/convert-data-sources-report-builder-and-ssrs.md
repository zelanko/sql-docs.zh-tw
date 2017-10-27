---
title: "轉換資料來源 （報表產生器及 SSRS） |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [Reporting Services], embedded
- data sources [Reporting Services], shared
ms.assetid: 0e099c7e-8c03-43eb-9ea3-76e52d9ebbe3
caps.latest.revision: 16
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: da3cd9531b90536283153b68642da9de01486a9b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="convert-data-sources-report-builder-and-ssrs"></a>轉換資料來源 (報表產生器和 SSRS)
  [報表資料] 窗格中的每個資料來源都是報表內嵌且專用的項目，或共用的項目。 在報表產生器中，共用資料來源會指向報表伺服器或 SharePoint 網站上的已發行共用資料來源。 在報表設計師中，共用資料來源會指向 [方案總管] 中 **[共用資料來源]** 資料夾的共用資料來源。  
  
 如需內嵌資料來源與共用資料來源之間差異的詳細資訊，請參閱[內嵌和共用資料連接或資料來源 &#40;報表產生器及 SSRS&#41;](http://msdn.microsoft.com/library/f417782c-b85a-4c4d-8a40-839176daba56)。  
  
 如需如何建立共用資料來源的詳細資訊，請參閱[建立內嵌或共用資料來源 &#40;SSRS&#41;](http://msdn.microsoft.com/library/b111a8d0-a60d-4c8b-b00a-51644b19c34b)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-designer"></a>報表設計師  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>若要將資料來源從內嵌轉換成共用  
  
-   在 [報表資料] 窗格中，以滑鼠右鍵按一下資料來源，然後按一下 [轉換成共用資料來源]。  
  
    > [!NOTE]  
    >  如果看不到 [報表資料] 窗格，請按一下 **[檢視]** 功能表上的 **[報表資料]**。 如果此窗格以浮動視窗的形式開啟，您可以將它停駐。 如需詳細資訊，請參閱[停駐報表設計師中的報表資料窗格 &#40;SSRS&#41;](../../reporting-services/tools/dock-the-report-data-pane-in-report-designer-ssrs.md)。  
  
     在 [報表資料] 窗格中，資料來源圖示會變成共用資料來源圖示。 在 [方案總管] 中，同名的共用資料來源會出現在 **[共用資料來源]** 資料夾底下。  
  
### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>若要將資料來源從共用轉換成內嵌  
  
-   在 [報表資料] 窗格中，以滑鼠右鍵按一下資料來源，開啟 [資料來源屬性] 對話方塊，然後按一下 [內嵌連接]。 接著，輸入必要的資訊。  
  
     在 [報表資料] 窗格中，資料來源圖示會變成共用資料來源圖示。  
  
## <a name="report-builder"></a>報表產生器  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>若要將資料來源從內嵌轉換成共用  
  
-   在 [報表資料] 窗格中，以滑鼠右鍵按一下資料來源開啟 [資料來源屬性] 對話方塊，然後按一下 [內嵌連接]。 接著，輸入必要的資訊。  
  
     在 [報表資料] 窗格中，資料來源圖示會變成共用資料來源圖示。  
  
#### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>若要將資料來源從共用轉換成內嵌  
  
-   在 [報表資料] 窗格中，以滑鼠右鍵按一下資料來源，開啟 [資料來源屬性] 對話方塊，然後按一下 [內嵌連接]。 接著，輸入必要的資訊。  
  
     在 [報表資料] 窗格中，資料來源圖示會變成共用資料來源圖示。  
  
## <a name="see-also"></a>請參閱＜  
 [管理報表資料來源](../../reporting-services/report-data/manage-report-data-sources.md)   
 [資料連接、資料來源及連接字串 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  

