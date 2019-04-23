---
title: 移動項目頁面 （報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: fc83b8d2-bc79-4b56-8970-34a1cbbcc176
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: acee0f51707a0535f0d6f63152cdf461ad50f46c
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59967744"
---
# <a name="move-items-page-report-manager"></a>移動項目頁面 (報表管理員)
  您可以使用 [移動項目] 頁面，將報表、資料夾或其他項目移至報表伺服器上的新位置。 您可以輸入新位置的路徑，或使用樹狀檢視以導覽到報表伺服器命名空間中的新位置。 您只能移動您有權移動並儲存在目前報表伺服器上的項目。  
  
 當您移動了其他項目所參考的項目 (例如，許多報表所參考的共用資料來源或模型) 時，系統就會自動更新該項目的路徑資訊。 移動共用資料來源並不會中斷使用此共用資料來源之報表和模型的資料來源連接。 如果您將共用資料來源移至使用者沒有權限的資料夾，他們仍然能夠執行參考此資料來源或模型的任何報表，不過他們在資料夾階層中將看不到該項目。  
  
 針對 **[位置]**，請指定資料夾的完整路徑，由根資料夾名稱開始。 您可以輸入路徑名稱，或使用樹狀檢視以導覽到適當的資料夾。  
  
> [!NOTE]  
>  並非所有項目都可以移動。 您不可以移動保留的資料夾，例如 [主資料夾]、[我的報表] 或 [使用者資料夾]。 您不可以將報表記錄或快照集移至其他位置。 記錄與快照集一律會置於所依據報表的位置，且一律需要透過該報表存取。  
  
## <a name="navigation"></a>巡覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
###### <a name="to-open-the-move-items-page-from-the-contents-page-in-details-view"></a>若要從詳細資料檢視的內容頁面開啟移動項目頁面  
  
1.  開啟報表管理員，然後導覽至包含您想要移動之項目的資料夾。 您也可以從報表管理員首頁移動項目。  
  
2.  在工具列中，按一下 **[詳細資料檢視]**。  
  
    > [!NOTE]  
    >  如果您只有看到 **[並排檢視]**，表示您已經在 **[詳細資料檢視]** 中。  
  
3.  選取項目旁的方塊，然後按一下工具列中的 **[移動]** 。 如果您想要將多個項目移至相同的新位置，也可以選取多個方塊。  
  
###### <a name="to-open-the-move-items-page-from-the-contents-page-in-tiles-view"></a>若要從並排檢視的內容頁面開啟移動項目頁面  
  
1.  開啟報表管理員，然後導覽至包含您想要移動之項目的資料夾。 您也可以從報表管理員首頁移動項目。  
  
2.  在工具列中，按一下 **[並排檢視]**。  
  
    > [!NOTE]  
    >  如果您只有看到 **[詳細資料檢視]**，表示您已經在 **[並排檢視]** 中。  
  
3.  將滑鼠停留在該項目上，然後按一下下拉箭號。  
  
4.  在下拉式功能表中，按一下 **[移動]**。  
  
###### <a name="to-open-the-move-items-page-from-the-general-properties-page-of-an-item"></a>若要從項目的一般屬性頁面開啟移動項目頁面  
  
1.  開啟報表管理員，然後導覽至包含您想要移動之項目的資料夾。 您也可以從報表管理員首頁移動項目。  
  
2.  將滑鼠停留在該項目上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[管理]**。 這樣就會開啟該項目的 [一般] 屬性頁面。  
  
4.  在項目工具列中，按一下 **[移動]**。  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [一般屬性頁面，資料夾&#40;報表管理員&#41;](../../2014/reporting-services/general-properties-page-folders-report-manager.md)   
 [一般屬性頁面，報表 &#40;報表管理員&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [一般屬性頁面、 資源&#40;報表管理員&#41;](../../2014/reporting-services/general-properties-page-resources-report-manager.md)   
 [一般屬性頁面、 共用資料來源&#40;報表管理員&#41;](../../2014/reporting-services/general-properties-page-shared-data-sources-report-manager.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
