---
title: 將量測計新增至報表 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 45da4fef-2b02-40e1-977c-f8f80d87155e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3e70b99c0918cd7121866b51a82bc9a5d9ae70c6
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56297366"
---
# <a name="add-a-gauge-to-a-report-report-builder-and-ssrs"></a>將量測計加入至報表 (報表產生器及 SSRS)
  在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表中，當您想要以視覺格式摘要列出資料時，可以使用量測計資料區域。 當您將量測計資料區加入至設計介面之後，就可以將報表資料集欄位拖曳到量測計的資料窗格。  
  
## <a name="to-add-a-gauge-to-your-report"></a>若要將量測計加入至報表  
  
1.  建立報表或開啟現有的報表。  
  
2.  在 [插入] 索引標籤上，按兩下 [量測計]。 **[選取量測計類型]** 對話方塊隨即開啟。  
  
3.  選取您想要加入的量測計類型。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  與圖表不同的是，量測計只有兩種類型：線性和星形。 **[選取量測計類型]** 對話方塊中的可用量測計是這兩種量測計類型的範本。 因此，當您將量測計加入至報表之後，就無法變更量測計類型。 您必須刪除並重新加入量測計，才能變更其類型。  
  
     如果報表沒有任何資料來源和資料集， **[資料來源屬性]** 對話方塊就會開啟並引導您完成建立這兩者的步驟。 如需詳細資訊，請參閱[新增及驗證資料連線 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
     如果報表具有資料來源，但是沒有任何資料集， **[資料集屬性]** 對話方塊就會開啟並引導您完成建立資料集的步驟。 如需詳細資訊，請參閱 [建立共用資料集或內嵌資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)。  
  
4.  按一下量測計，即可顯示資料窗格。 根據預設，量測計具有對應至某個值的單一指標。 您還可以加入其他指標。  
  
5.  將一個欄位從資料集加入至資料欄位放置區。 您只能加入一個欄位。 如果您想要顯示多個欄位，您必須加入其他指標 (每一個欄位一個指標)。  
  
     以滑鼠右鍵按一下量測計標尺，然後選取 [標尺屬性]。 針對標尺的 **[最小值]** 和 **[最大值]** 輸入值。 如需詳細資訊，請參閱[設定量測計的最小值或最大值 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [巢狀資料區 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)   
 [量測計 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  
