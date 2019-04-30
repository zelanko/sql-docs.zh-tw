---
title: 檢查更新或關閉更新 （報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 9c69792d-d7c4-453b-ae2f-6d2d071d8606
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ae7f72240148291504654fffa304ebda252178ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63266064"
---
# <a name="check-for-updates-or-turn-updates-off-report-builder-and-ssrs"></a>檢查更新或關閉更新 (報表產生器及 SSRS)
  每當您開啟報表時，報表產生器都會檢查報表伺服器或與報表伺服器整合的 SharePoint 網站上是否已經更新該報表中已發行的報表組件執行個體。 它也會檢查報表組件的相依項目 (如資料集和參數) 是否有變更。 如果網站或伺服器上已經更新任何報表組件或其相依性，報表中的資訊列會顯示更新的組件數。 您可以選擇檢視並接受或拒絕更新，或是解除資訊列。  
  
 您也可以停用資訊列，如此一來，當已發行的報表組件執行個體變更時，您將不會收到通知。 這是一項使用者設定，您所開啟的所有報表都會停用這項設定。 即使您停用了資訊列，還是可以檢查更新。  
  
### <a name="to-turn-on-and-off-report-part-updates"></a>若要開啟和關閉報表組件更新  
  
1.  按一下 [報表產生器] 按鈕，然後按一下**選項**。  
  
2.  在 **選項**對話方塊的 **資源**索引標籤上，選取或清除**在我的報表中顯示的報表組件的更新**核取方塊。  
  
> [!NOTE]  
>  這是使用者設定。 您所開啟的所有報表都會停用這項設定。  
  
### <a name="to-check-for-updates"></a>若要檢查更新  
  
-   以滑鼠右鍵按一下報表外面，或在報表主體中，在設計介面，然後按一下 **檢查是否有更新**。  
  
## <a name="see-also"></a>另請參閱  
 [報表組件 &#40;報表產生器及 SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [發行與重新發行報表組件&#40;報表產生器及 SSRS&#41;](report-design/publish-and-republish-report-parts-report-builder-and-ssrs.md)   
 [瀏覽報表組件及設定預設資料夾&#40;報表產生器及 SSRS&#41;](report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)   
 [疑難排解報表組件&#40;報表產生器及 SSRS&#41;](../../2014/reporting-services/troubleshoot-report-parts-report-builder-and-ssrs.md)   
 [報表產生器中的報表組件和資料集](report-data/report-parts-and-datasets-in-report-builder.md)  
  
  
