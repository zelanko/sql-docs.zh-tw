---
title: 建立、 刪除或修改資料夾-Reporting Services |Microsoft Docs
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: 70a38879-856c-414b-8479-5f9dead38f15
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 874fb7ba143c8f08a0f25501e1852b4d2b280cb2
ms.sourcegitcommit: c0e48b643385ce19c65ca6e348ce83b2d22b6514
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492858"
---
# <a name="create-delete-or-modify-a-folder---reporting-services"></a>建立、 刪除或修改資料夾-Reporting Services
  您可以建立資料夾來組織與管理發行至報表伺服器的項目。 建立資料夾可以協助使用者尋找他們感興趣的報表。 對於內容管理員而言，資料夾會提供套用權限的架構。 您可以針對特定資料夾建立角色指派，以便限制在開發中或不應該廣為散發之報表的存取權。  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

## <a name="to-create-a-folder"></a>若要建立資料夾  
  
1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)。  
  
2.  在報表管理員中，選取主資料夾，然後按一下 [新增資料夾]  。 或者若要在現有資料夾下建立資料夾，請在 [內容]  頁面中巡覽到該資料夾，然後按一下資料夾以開啟資料夾。 接著按一下 [新增資料夾]  。  
  
     [新增資料夾]  頁面隨即開啟。  
  
3.  輸入資料夾名稱。 資料夾名稱可以包含空格，但是不能包含用於 URL 編碼的保留字元：\;\? \: \@ \& \= \+ \, \$ \/ \* \< \> \|。 您無法一次輸入一連串的資料夾名稱來建立數個資料夾。  
  
4.  選擇性地輸入描述。  
  
5.  如果您不要在 [內容]  頁面的預設檢視中顯示資料夾，請選取 [在清單檢視中隱藏]  。 使用者只有在按一下 [內容]  頁面上的 [顯示詳細資料]  時，才看得到資料夾。  
  
6.  按一下 [確定]  。  
  
## <a name="to-delete-a-folder"></a>若要刪除資料夾  
  
1.  在報表管理員中，巡覽到 [內容]  頁面，然後找出您要修改的項目。  
  
2.  將滑鼠停留在該項目上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 [刪除]  。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-modify-or-delete-a-folder"></a>若要修改或刪除資料夾  
  
1.  在報表管理員中，巡覽到 [內容]  頁面，然後找出您要修改的項目。  
  
2.  將滑鼠停留在該項目上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[管理]** 。 [一般屬性] 頁面隨即開啟。  
  
4.  若要變更資料夾位置，請按一下 [移動]  。 鍵入目的資料夾的位置，或者從樹狀目錄中選擇目的資料夾，然後按一下 [確定]  。  
  
5.  或者，利用下列方式修改資料夾屬性：  
  
    -   若要修改有關資料夾的顯示文字，請輸入名稱或描述。  
  
    -   若要在 [內容]  頁面的預設檢視中顯示資料夾，請清除 [在清單檢視中隱藏]  。  
  
6.  或者，若要移除資料夾及其內容，請按一下 [刪除]  。  
  
7.  按一下 [套用]  儲存變更。  

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
 
## <a name="to-create-a-folder"></a>若要建立資料夾  
  
1. 開啟[報表伺服器的入口網站 (SSRS 原生模式)](../../reporting-services/web-portal-ssrs-native-mode.md)。  
  
2. 瀏覽至資料夾或您想要用來找出新的資料夾的子資料夾。 選取 **首頁**藉由選取的資料夾**瀏覽**在頂端工具列上的按鈕保留的頁面，即可建立在資料夾階層的頂端。  
  
3. 選取 **的新**頂端的 報表伺服器 工具列中，然後再選取**資料夾**從下拉式選單。  
  
4. 在  **（目前的資料夾名稱） 中建立新的資料夾**對話方塊方塊中，輸入要建立新資料夾的名稱。 資料夾名稱可以包含空格，但是不能包含用於 URL 編碼的保留字元：\; \? \: \@ \& \= \+ \, \$ \/ \* \< \> \|。 您也不可為了建立數個資料夾，而一次鍵入一連串資料夾名稱。  
  
5. 選取 **建立**以完成動作。  
  
## <a name="to-delete-a-folder"></a>若要刪除資料夾  
  
1. 在入口網站中，瀏覽資料夾階層並找出您想要刪除的資料夾。  
  
2. 右邊-click 的資料夾，然後選取**刪除**從下拉式選單。  
  
3. 選取 **刪除**按鈕**刪除<foldername>** 對話方塊中，以確認刪除。  
  
## <a name="to-modify-a-folders-properties"></a>若要修改資料夾屬性  
  
1. 在入口網站中，瀏覽資料夾階層並找出您想要刪除的資料夾。  
  
2. 右邊-click 的資料夾，然後選取**刪除**從下拉式選單。  
  
3. 選取 [屬性]  索引標籤。**屬性**預設會顯示頁面。  
  
4. 您可以變更的資料夾名稱*名稱** 文字方塊中。  
  
5. 您可以新增或變更的資料夾中的說明*描述** 文字方塊中。  
  
6. 您可以隱藏或取消隱藏的資料夾，藉由檢查或取消選取**隱藏此項目**核取方塊分別。  
  
7. 選取 **套用**儲存屬性變更。  
  
8. （選擇性） 您可以移動或刪除選取的資料夾**移動**或是**刪除**頂端的按鈕**屬性**頁面。 請參閱[移動或刪除項目 （web 入口網站）](../../reporting-services/report-server/move-or-delete-an-item-report-manager.md)文件，如需詳細資訊。  
  
## <a name="see-also"></a>另請參閱  
 [建立、刪除或修改資料夾 (入口網站)](../../reporting-services/report-server/create-delete-or-modify-a-folder-web-portal.md)   
 [報表伺服器內容管理 (SSRS 原生模式)](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)    
  
::: moniker-end