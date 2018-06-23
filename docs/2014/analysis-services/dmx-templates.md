---
title: DMX 範本 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2a577e52-821d-4bd3-ba35-075a6be285c9
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d0f29e0c000477ec705111f433c31370edc0d973
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137188"
---
# <a name="dmx-templates"></a>DMX 範本
  資料採礦範本可幫助您快速建立複雜的查詢。 雖然 DMX 查詢的一般語法已完整記載，但是使用範本可直接按一下並指向引數和資料來源，讓您更容易建立查詢。  
  
## <a name="using-the-templates"></a>使用範本  
  
1.  適用於 Excel 的資料採礦用戶端，請按一下**查詢**。  
  
2.  在精靈**啟動**頁面上，按一下**下一步**。  
  
3.  在頁面上，**選取模型**，按一下 **進階**。  
  
     **提示：** 如果您要在模型上建立預測查詢，您可以先選取模型，然後按一下**進階**，以預先填入範本使用的模型名稱。  
  
4.  在**資料採礦進階查詢編輯器**，按一下  **DMX 範本**，然後選取範本。  
  
5.  按 ENTER 將範本載入 [DMX 查詢] 窗格中。  
  
6.  繼續按一下範本中的連結，然後在對話方塊出現時，選取適當的輸出、模型或參數。  
  
     若是預測查詢，請先選擇輸入資料集，再對應資料行。  
  
7.  按一下**編輯查詢**切換到文字編輯器檢視，並手動變更查詢。  
  
     但是請注意，如果您在使用查詢編輯器時切換檢視，便會清除在上一個檢視中的所有資訊。 在變更檢視之前，請將 DMX 陳述式複製並貼到另一個檔案以儲存您的工作。  
  
8.  按一下 **[完成]**。 在**選擇目的地**對話方塊方塊中，指定您想要儲存的結果。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
> [!NOTE]  
>  如果您已成功地執行陳述式，傳送到伺服器的 DMX 陳述式也會記錄在**追蹤**視窗。 如需如何使用追蹤功能的詳細資訊，請參閱[追蹤&#40;適用於 Excel 的資料採礦用戶端&#41;](trace-data-mining-client-for-excel.md)。  
  
 如需如何使用資料採礦進階查詢編輯器的詳細資訊，請參閱[查詢&#40;SQL Server 資料採礦增益集&#41;](query-sql-server-data-mining-add-ins.md)和[進階資料採礦查詢編輯器](advanced-data-mining-query-editor.md)。  
  
## <a name="list-of-dmx-templates"></a>DMX 範本的清單  
 適用於 Excel 的資料採礦用戶端中包括下列 DMX 範本。  
  
 **預測**  
  
 使用這些範本可建立進階預測查詢，包括增益集精靈不支援的查詢，例如，使用巢狀資料表或外部資料來源的查詢。  
  
-   篩選的預測  
  
-   篩選的巢狀預測  
  
-   巢狀預測  
  
-   單一預測  
  
-   標準預測  
  
-   時間序列預測  
  
-   TOP 預測查詢  
  
-   巢狀資料表上的 TOP 預測查詢  
  
 **建立**  
  
 使用這些範本可建立自訂模型或資料結構。 您不受限於精靈支援的模型，可以使用所連接 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體支援的所有資料採礦演算法，包括外掛程式演算法。  
  
-   採礦模型  
  
-   採礦結構  
  
-   含鑑效組的採礦結構  
  
-   暫時性模型  
  
-   暫時性結構  
  
 **模型屬性**  
  
 使用這些範本可建立查詢，取得有關模型和定型集的中繼資料。 您也可以從模型內容擷取詳細資料，或是取得定型資料的統計資料設定檔。  
  
-   採礦模型內容  
  
-   最小和最大資料行的值  
  
-   採礦結構測試/定型案例  
  
-   離散資料行的值  
  
 **管理**  
  
 使用這些範本可執行 DMX 支援的所有管理工作，包括匯入與匯出模型、刪除模型，以及清除模型或資料結構。  
  
-   清除採礦模型  
  
-   清除結構和模型  
  
-   清除採礦結構  
  
-   刪除採礦模型  
  
-   刪除採礦結構  
  
-   重新命名採礦模型  
  
-   重新命名採礦結構  
  
-   定型採礦模型  
  
-   定型巢狀採礦結構  
  
-   定型採礦結構  
  
### <a name="requirements"></a>需求  
 根據您使用的範本而定，您可能需要系統管理權限才能存取 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器並執行查詢。  
  
## <a name="see-also"></a>另請參閱  
 [建立資料採礦模型](creating-a-data-mining-model.md)  
  
  