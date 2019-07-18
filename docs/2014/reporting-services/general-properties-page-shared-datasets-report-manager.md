---
title: 一般屬性頁面、 共用資料集 （報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 10798e41-24c3-4e69-893b-7ee6af7fc958
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bf433f27a5d8dc7f5e0efcf6f5774ed292d1e1a1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109071"
---
# <a name="general-properties-page-shared-datasets-report-manager"></a>一般屬性頁面、共用資料集 (報表管理員)
  使用 [共用資料集] 頁面，即可檢視及管理共用資料集項目的屬性。  
  
 您無法從報表管理員檢視或變更共用資料集定義，包括查詢在內。 若要變更定義，您必須使用撰寫工具來開啟及修改定義，然後將該定義儲存至報表伺服器。  
  
 您可以使用共用資料集，從報表、元件及其他使用該資料集的目錄項目，個別管理資料集的設定。  
  
## <a name="navigation"></a>巡覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
###### <a name="to-open-the-shared-dataset-properties-page-for-a-shared-dataset"></a>開啟共用資料集的共用資料集屬性頁面  
  
1.  開啟報表管理員，然後找出您想要設定屬性的共用資料集。  
  
2.  將滑鼠停留在共用資料集上方，然後按下拉式箭號。  
  
3.  在下拉式清單中，按一下 **[管理]** ， 就會開啟 [一般] 屬性頁面。  
  
## <a name="options"></a>選項  
 **名稱**  
 輸入可用來識別報表伺服器資料夾階層中項目的共用資料集名稱。  
  
 **說明**  
 提供有關共用資料集的資訊。 此描述會顯示在 [內容] 頁面上。  
  
 **在清單檢視中隱藏**  
 隱藏共用資料集，避免在報表管理員中使用清單檢視模式的使用者看見。 清單檢視模式是瀏覽報表伺服器資料夾階層時的預設檢視格式。 在清單檢視中，項目名稱和描述會跨頁排列。 替代格式是詳細資料檢視。 詳細資料檢視會省略描述，但會包括項目的其他相關資訊。 雖然在清單檢視中可以隱藏項目，但在詳細資料檢視中則不行。 如果想要限制項目的存取，您必須建立角色指派。  
  
 **查詢執行逾時**  
 輸入查詢逾時之前的秒數。如果是 0，則查詢不會逾時。  
  
 **Apply**  
 儲存變更。  
  
 **刪除**  
 從報表伺服器資料庫中移除共用資料集。 刪除共用資料集會停用任何報表或快取版本。 若要重新啟動報表，您必須在報表撰寫工具中開啟每一個報表，並指定具有相同名稱和相同欄位集合的資料集。 或者，您也可以更新每個資料區參考，以使用含相同欄位集合的不同資料集。  
  
 **[移動]**  
 將報表伺服器資料夾階層內的共用資料集重新定位放置。 按一下此按鈕會開啟 [移動項目] 頁面，您可在此瀏覽資料夾以選取新位置。 如需詳細資訊，請參閱 <<c0> [ 移動項目頁面&#40;報表管理員&#41;](../../2014/reporting-services/move-items-page-report-manager.md)。</c0>  
  
 **下載**  
 擷取共用資料集定義的複本。 視電腦上定義的檔案關聯而定，檔案會在 Visual Studio 或其他應用程式中開啟。 在大多數情況下，共用資料集會開啟為 XML 檔案。  
  
 **取代**  
 使用位於檔案系統中 .rsd 檔案的不同資料集定義，取代共用資料集定義。  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [內容頁面 &#40;報表管理員&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)   
 [快取重新整理選項&#40;報表管理員&#41;](../../2014/reporting-services/cache-refresh-options-report-manager.md)   
 [快取頁面、 共用資料集&#40;報表管理員&#41;](../../2014/reporting-services/caching-page-shared-datasets-report-manager.md)   
 [管理共用資料集](report-data/manage-shared-datasets.md)   
 [快取共用資料集 &#40;SSRS&#41;](report-server/cache-shared-datasets-ssrs.md)  
  
  
