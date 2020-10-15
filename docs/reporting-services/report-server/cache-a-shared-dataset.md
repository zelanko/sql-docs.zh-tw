---
title: 快取共用資料集 | Microsoft Docs
description: 了解如何針對報表管理員中快取共用資料集的到期日進行排程。 快取共用資料集可改善效能。
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: c2d8c81a-da1e-4a8a-9845-fff9a0903d24
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 24bfa991596630165675bc0c8349a04c76085420
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987194"
---
# <a name="cache-a-shared-dataset"></a>快取共用資料集
  改善效能的其中一種方式就是設定共用資料集的快取屬性。 快取共用資料集時，系統會在一段指定的時間內儲存查詢結果的副本。 要求使用共用資料集之報表的第一位使用者必須等候查詢結果以及所有處理都完成，然後才能檢視該報表。 在快取期間內要求該報表的後續使用者將會立即體驗到增進的效能，因為查詢和處理都已經進行了。 您也可以指定執行查詢的快取重新整理計劃，並在指定的快取逾期前快取結果。  
  
 根據共用資料集或快取重新整理計劃執行報表的使用者會建立查詢快取，而且在這兩種情況下，都可以根據快取逾期選項使用快取。  
  
 您可以快取的共用資料集類型有所限制。 例如，如果資料會因使用者識別而不同，或者資料是使用要求報表之使用者的安全性 Token 擷取的，系統就無法快取該查詢結果。 如需詳細資訊，請參閱[快取共用資料集 &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md) 和[快取多個報表 &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)。  
  
### <a name="to-schedule-the-expiration-of-a-cached-report"></a>若要排程快取報表的逾期  
  
1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;](../web-portal-ssrs-native-mode.md)。  
  
2.  在報表管理員中，導覽至您想要設定快取屬性的共用資料集、將滑鼠停留在該項目上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[管理]** 。  
  
4.  在左框架內，按一下 **[快取]** 。  
  
    > [!NOTE]  
    >  如果您看到「 **尚未儲存用來執行共用資料集的認證**」這個錯誤，將會停用快取共用資料集選項。 您需要修改資料來源來儲存認證，或修改共用資料集來使用與儲存認證不同的資料來源。  
  
5.  選取 **[快取共用資料集]** 。  
  
6.  選取快取於 30 分鐘後過期的選項。 您也可以選擇讓快取在指定的排程時間過期。  
  
7.  按一下 [套用]。  
  
## <a name="see-also"></a>另請參閱  
 [管理共用資料集](../../reporting-services/report-data/manage-shared-datasets.md)  
  
