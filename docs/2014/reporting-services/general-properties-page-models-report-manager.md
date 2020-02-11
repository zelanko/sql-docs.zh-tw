---
title: 一般屬性頁面、模型（報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.modelproperties.general.f1
ms.assetid: 7ad59850-8135-4c4d-95e9-6d705b6d77a8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 815b8594977321ea8223c16fed166e110008a8b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109105"
---
# <a name="general-properties-page-models-report-manager"></a>一般屬性頁面，模型 (報表管理員)
  您可以使用報表模型的 [一般屬性] 頁面來重新命名、刪除、移動或取代模型定義 (.smdl) 檔案。 有關模型建立者與修改者及變更日期的詳細資料都會顯示在頁面頂端。  
  
## <a name="navigation"></a>導覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
###### <a name="to-open-the-general-properties-page-for-a-model"></a>若要開啟模型的一般屬性頁面  
  
1.  開啟報表管理員，然後找出您想要檢視或設定屬性的模型。  
  
2.  將滑鼠停留在該模型上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[管理]** 。 這樣就會開啟該模型的 [一般] 屬性頁面。  
  
## <a name="options"></a>選項。  
 **名稱**  
 指定模型的名稱。 名稱必須至少包含一個英數字元。 它也可以包含空格和某些符號。 指定名稱時，請勿使用下列字元：  
  
 ; ? ： \@ & = +，$/* \< > |" /  
  
 **說明**  
 輸入模型的描述。 這項描述會顯示在有權存取此模型之使用者的 [內容] 頁面上。  
  
 **在清單檢視中隱藏**  
 選取此核取方塊即可在清單檢視中設定資料夾時，隱藏項目。 清單檢視是檢視資料夾內容的一種模式，報表管理員中支援這種檢視模式。 您可以在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 中設定這個選項，以便定義在報表管理員中檢視這個項目的方式。 如需報表管理員中視圖模式的詳細資訊，請參閱[內容頁面 &#40;報表管理員&#41;](../../2014/reporting-services/contents-page-report-manager.md)。  
  
 **套用**  
 按一下即可儲存您的變更。  
  
 **刪除**  
 按一下即可從報表伺服器資料庫中移除模型。 刪除模型並不會刪除提供連接資訊的相依共用資料來源，也不會刪除使用此模型當做資料來源的報表。 不過，刪除模型之後，使用該模型的報表將無法再執行。  
  
 **移動**  
 按一下即可在報表伺服器資料夾階層內重新定位模型。 按一下此按鈕會開啟 [移動項目] 頁面，您可在此瀏覽資料夾以選取新位置。 如需詳細資訊，請參閱[&#40;報表管理員&#41;中移動專案頁面](../../2014/reporting-services/move-items-page-report-manager.md)。  
  
 **另**  
 按一下即可儲存模型定義的唯讀副本。 視電腦上定義的檔案關聯而定，系統會在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 或其他應用程式中開啟檔案。 在大多數情況下，系統會將模型開啟為 XML 檔案。  
  
 您開啟的副本與初始發行至報表伺服器的原始模型定義相同。 發行模型之後在模型上設定的任何屬性 (例如資料來源屬性) 都不會反映在您開啟的檔案中。  
  
 您可以修改模型定義並在共用資料夾中另存新檔，然後將模型定義上傳到報表伺服器當做新項目。 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] (或其他應用程式) 中開啟模型定義時，您對模型定義所做的修改並不會直接儲存到報表伺服器中。 您必須上傳檔案，才能將修改的模型發行到報表伺服器。  
  
 請注意，如果您想要在模型設計師中開啟此報表模型，就應該將此模型儲存成 .smdl 檔案，然後在模型設計師中，將此 .smdl 檔案加入至專案。  
  
 **取代**  
 按一下即可使用位於檔案系統中 .smdl 檔案的不同模型定義，取代此模型定義。 如果您更新了模型定義，就必須在完成更新之後重設共用資料來源設定。  
  
 **重新產生模型**  
 按一下即可重新產生取代目前版本的預設模型。 這個選項會在產生模型之後顯示。 產生的模型是以共用資料來源為基礎。 您無法在它產生之前進行自訂。 不過，當您產生它之後，就可以按一下 **[編輯]** 開啟模型定義、將它儲存至檔案系統，然後在模型設計師中，將它加入至專案。 當您修改模型之後，可以將它上傳至報表伺服器當做新項目，也可以按一下這個頁面上的 **[更新]** ，使用您在模型設計師中修訂的版本來取代產生的模型。  
  
## <a name="see-also"></a>另請參閱  
 [將報表或模型系結至 &#40;SSRS&#41;的共用資料來源](report-data/bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [Management Studio F1 說明中的報表伺服器](tools/report-server-in-management-studio-f1-help.md)  
  
  
