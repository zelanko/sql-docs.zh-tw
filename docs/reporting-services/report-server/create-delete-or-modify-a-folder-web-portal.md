---
title: 建立、刪除或修改資料夾 - Reporting Services | Microsoft Docs
description: 了解如何建立、修改和刪除資料夾，以供組織及管理發佈至 Reporting Services 報表伺服器的項目。
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: 70a38879-856c-414b-8479-5f9dead38f15
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e1c2094a4ee16d33c6e076440e56a55434b2347a
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987184"
---
# <a name="create-delete-or-modify-a-folder---reporting-services"></a>建立、刪除或修改資料夾 - Reporting Services
  您可以建立資料夾來組織與管理發行至報表伺服器的項目。 建立資料夾可以協助使用者尋找他們感興趣的報表。 對於內容管理員而言，資料夾會提供套用權限的架構。 您可以針對特定資料夾建立角色指派，以便限制在開發中或不應該廣為散發之報表的存取權。  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

## <a name="to-create-a-folder"></a>若要建立資料夾  
  
1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;](../web-portal-ssrs-native-mode.md)。  
  
2.  在報表管理員中，選取主資料夾，然後按一下 [新增資料夾]。 或者若要在現有資料夾下建立資料夾，請在 [內容]**** 頁面中巡覽到該資料夾，然後按一下資料夾以開啟資料夾。 接著按一下 [新增資料夾]。  
  
     [新增資料夾] 頁面隨即開啟。  
  
3.  輸入資料夾名稱。 資料夾名稱可以包含空格，但是不能包含用於 URL 編碼的保留字元：\; \? \: \@ \& \= \+ \, \$ \/ \* \< \> \|. 您無法一次輸入一連串的資料夾名稱來建立數個資料夾。  
  
4.  選擇性地輸入描述。  
  
5.  如果您不要在 [內容] 頁面的預設檢視中顯示資料夾，請選取 [在清單檢視中隱藏]。 使用者只有在按一下 [內容] 頁面上的 [顯示詳細資料] 時，才看得到資料夾。  
  
6.  按一下 [確定]。  
  
## <a name="to-delete-a-folder"></a>若要刪除資料夾  
  
1.  在報表管理員中，巡覽到 [內容] 頁面，然後找出您要修改的項目。  
  
2.  將滑鼠停留在該項目上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 [刪除]。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-modify-or-delete-a-folder"></a>若要修改或刪除資料夾  
  
1.  在報表管理員中，巡覽到 [內容] 頁面，然後找出您要修改的項目。  
  
2.  將滑鼠停留在該項目上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[管理]** 。 [一般屬性] 頁面隨即開啟。  
  
4.  若要變更資料夾位置，請按一下 [移動]。 鍵入目的資料夾的位置，或者從樹狀目錄中選擇目的資料夾，然後按一下 [確定]。  
  
5.  或者，利用下列方式修改資料夾屬性：  
  
    -   若要修改有關資料夾的顯示文字，請輸入名稱或描述。  
  
    -   若要在 [內容] 頁面的預設檢視中顯示資料夾，請清除 [在清單檢視中隱藏]。  
  
6.  或者，若要移除資料夾及其內容，請按一下 [刪除]。  
  
7.  按一下 [套用] 以儲存變更。  

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
 
## <a name="to-create-a-folder"></a>若要建立資料夾  
  
1. 開啟[報表伺服器的入口網站 (SSRS 原生模式)](../../reporting-services/web-portal-ssrs-native-mode.md)。  
  
2. 巡覽至您想要在其中尋找新資料夾的資料夾或子資料夾。 選取 [主資料夾]**** 資料夾，方法是選取頁面左上角工具列上的 [瀏覽]**** 按鈕，以在資料夾階層的頂端建立該資料夾。  
  
3. 選取報表伺服器工具列右上方的 [新增] 按鈕，然後從下拉式功能表中選取 [資料夾]。  
  
4. 於 [在 (目前的資料夾名稱) 中建立新資料夾] 對話方塊中，輸入要建立的新資料夾名稱。 資料夾名稱可以包含空格，但是不能包含用於 URL 編碼的保留字元：\; \? \: \@ \& \= \+ \, \$ \/ \* \< \> \|. 您也不可為了建立數個資料夾，而一次鍵入一連串資料夾名稱。  
  
5. 選取 [建立]以完成動作。  
  
## <a name="to-delete-a-folder"></a>若要刪除資料夾  
  
1. 在入口網站中，巡覽資料夾階層，並找出您想要刪除的資料夾。  
  
2. 以滑鼠右鍵按一下資料夾，然後從下拉式功能表中選取 [刪除]。  
  
3. 選取 [刪除 <foldername>] 對話方塊中的 [刪除] 按鈕以確認刪除。  
  
## <a name="to-modify-a-folders-properties"></a>修改資料夾的屬性  
  
1. 在入口網站中，巡覽資料夾階層，並找出您想要刪除的資料夾。  
  
2. 以滑鼠右鍵按一下資料夾，然後從下拉式功能表中選取 [刪除]。  
  
3. 選取 [屬性] 索引標籤。預設會出現 [屬性] 頁面。  
  
4. 您可以在 [名稱]* 文字方塊中變更資料夾的名稱。  
  
5. 您可以在 [描述]* 文字方塊中，新增或變更資料夾的描述。  
  
6. 您可以藉由核取或取消核取 [隱藏此項目] 核取方塊來隱藏或取消隱藏資料夾。  
  
7. 選取 [套用] 以儲存屬性變更。  
  
8. 或者，您可以選取 [屬性] 頁面頂端的 [移動] 或 [刪除] 按鈕來移動或刪除資料夾。 如需詳細資訊，請參閱[移動或刪除項目 (入口網站)](../../reporting-services/report-server/move-or-delete-an-item-report-manager.md) 一文。  
  
## <a name="see-also"></a>另請參閱  
 [建立、刪除或修改資料夾 (入口網站)](../../reporting-services/report-server/create-delete-or-modify-a-folder-web-portal.md)   
 [報表伺服器內容管理 (SSRS 原生模式)](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)    
  
::: moniker-end