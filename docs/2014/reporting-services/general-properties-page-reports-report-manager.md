---
title: 一般屬性頁面，報表 （報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 66c99d28-ab41-45f0-bf02-ed560293595d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e8606f2ee9afeb0e5e3ab0663290471b0d2d4463
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48206160"
---
# <a name="general-properties-page-reports-report-manager"></a>一般屬性頁面，報表 (報表管理員)
  使用報表的 [一般] 屬性頁面，即可重新命名、刪除、移動或取代報表定義。 您也可以使用此頁面來建立連結報表。 在頁面頂端指出有關建立或修改報表的人員，以及發生變更之時間的詳細資料。  
  
## <a name="navigation"></a>導覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
###### <a name="to-open-the-general-properties-page-for-a-report"></a>若要開啟報表的一般屬性頁面  
  
1.  開啟報表管理員，然後找出您想要檢視或設定屬性的報表。  
  
2.  將滑鼠停留在該報表上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[管理]**。 這樣就會開啟該報表的 [一般] 屬性頁面。  
  
## <a name="options"></a>選項。  
 **名稱**  
 指定報表的名稱。 名稱必須至少包含一個英數字元。 也可以包含空格和特定符號。 請勿使用 ; ? : \@ & = +，$ * \< >  
  
 " 或 / (在指定名稱時)。  
  
 **說明**  
 輸入報表的描述。 此描述顯示在有權存取此報表的使用者的 [內容] 頁面上。  
  
 **在清單檢視中隱藏**  
 選取這個選項可以對正在「報表管理員」中使用清單檢視模式的使用者隱藏報表。 清單檢視模式是瀏覽報表伺服器資料夾階層時的預設檢視格式。 在清單檢視中，項目名稱和描述會跨頁排列。 替代格式是詳細資料檢視。 詳細資料檢視會省略描述，但會包括項目的其他相關資訊。 雖然在清單檢視中可以隱藏項目，但在詳細資料檢視中則不行。 如果想要限制項目的存取，您必須建立角色指派。  
  
 **套用**  
 按一下即可儲存您的變更。  
  
 **刪除**  
 按一下即可從報表伺服器資料庫中移除報表。 刪除報表會刪除所有相關聯的報表記錄和報表特定排程與訂閱。 如果報表與連結報表相關聯，則該連結報表無效。  
  
 **[移動]**  
 按一下即可在報表伺服器資料夾階層內重新定位報表。 按一下此按鈕會開啟 [移動項目] 頁面，您可在此瀏覽資料夾以選取新位置。 如需詳細資訊，請參閱 <<c0> [ 移動項目頁面&#40;報表管理員&#41;](../../2014/reporting-services/move-items-page-report-manager.md)。</c0>  
  
 **建立連結的報表**  
 按一下即可開啟 [新增連結報表] 頁面。 如需有關此頁面和連結的報表的詳細資訊，請參閱 <<c0> [ 新增連結報表頁面&#40;報表管理員&#41;](../../2014/reporting-services/new-linked-report-page-report-manager.md)。</c0>  
  
 **儲存**  
 按一下即可擷取報表定義的唯讀副本。 視電腦上定義的檔案關聯而定，系統會在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 或其他應用程式中開啟檔案。 在大多數情況下，會將報表開啟為 XML 檔案。  
  
 您開啟的副本與初始發行至報表伺服器的原始報表定義相同。 發行報表之後，在報表上設定的任何屬性 (例如參數和資料來源屬性)，都不會反映在您開啟的檔案中。  
  
 您可以修改報表定義並在共用資料夾中另存新檔，然後將報表定義上傳到報表伺服器作為新項目。 您對報表定義中開啟時進行的修改[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]（或另一個應用程式） 並不直接儲存到報表伺服器。 您必須上傳檔案，才能將修改的報表發行到報表伺服器。  
  
 **取代**  
 按一下即可使用位於檔案系統中 .rdl 檔案的不同報表定義，取代目前報表中使用的報表定義。 若要更新報表定義，必須在完成更新之後重設資料來源設定。  
  
 **變更連結**  
 按一下即可針對連結報表選取不同的報表定義。 如果報表是連結報表，就會出現此選項。 如果報表是連結報表，您可以設定此屬性來取代報表定義。  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員&#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
