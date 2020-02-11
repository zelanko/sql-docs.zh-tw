---
title: 變更屬性類型 (適用於 Excel 的 MDS 增益集) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9d3001d9-8d0f-4e4a-8e04-4f666bf0df69
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4406eb225002bbf5df93f8c67385694922d7d2c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65482759"
---
# <a name="change-the-attribute-type-mds-add-in-for-excel"></a>變更屬性類型 (適用於 Excel 的 MDS 增益集)
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，當資料類型或是允許的字元數目不正確時，管理員可以變更屬性類型。  
  
 如果您想要變更屬性類型來建立受條件約束的清單 (網域屬性)，請參閱[建立網域屬性 &#40;適用於 Excel 的 MDS 增益集&#41;](create-a-domain-based-attribute-mds-add-in-for-excel.md)。  
  
> [!NOTE]  
>  您不能更新 **Name** 或 **Code** 資料行的類型或長度。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 [系統管理]**** 和總管**** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](../administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
-   必須有現有的模型、實體和屬性存在。  
  
### <a name="to-change-the-attribute-type"></a>若要變更屬性類型  
  
1.  在 Excel 中，載入包含您想要變更之資料行 (屬性) 的實體。 如需詳細資訊，請參閱將[資料從 MDS 載入 Excel](export-data-to-excel-from-master-data-services.md)中。  
  
2.  在您想要變更的資料行中按一下任何資料格。  
  
3.  在 [建立模型]**** 群組中，按一下 [屬性內容]****。  
  
4.  在 [屬性內容]**** 對話方塊中，視需要更新設定。  
  
5.  按一下 [確定]  。  
  
## <a name="what-happens-when-you-change-the-attribute-type"></a>當您變更屬性類型時會發生什麼情況？  
 如果有屬性的相依性，例如屬性由任何 MDS 商務規則參考或屬性包含在訂閱檢視中，而且您變更屬性的資料類型，則 MDS 會：  
  
-   變更屬性的資料類型。  
  
-   產生具有後置詞 "_old" 且不含任何值的屬性複本。 這稱為已被**取代**的屬性。  
  
 不過，原始屬性的所有現有相依性會指向已被取代的屬性，而不會指向變更的屬性。  
  
 這表示：  
  
-   因為在屬性的新資料類型中邏輯可能不同，您必須重新整理商務規則，指向已變更的屬性。 您將需要編輯每個受影響的規則，然後重新組織運算式，以便移除已被取代之屬性 (_old) 的參考，指向更新屬性。  
  
-   您必須開啟 [整合管理] 選取範圍下的任何訂用帳戶，選取 [view] 資料列，然後按一下鉛筆圖示以開啟它進行編輯，然後按一下 [**儲存檔**] 圖示來重新整理視圖定義。 重新產生檢視語法不需要其他變更。  
  
-   包含屬性的暫存資料表會加入一個已被取代的屬性資料行，這表示您的暫存碼會受到影響。 若要移除已被取代的屬性，您可以在更新了商務規則和訂閱檢視之後刪除它。  
  
 **刪除已被取代的屬性**  
  
 刪除任何已被取代的屬性之前，您必須移除屬性的任何參考 (例如修正商務規則和重新產生訂閱檢視)，如前文所述。 否則，當您嘗試刪除已被取代的屬性時，系統管理網頁上會發生錯誤，表示屬性由物件參考，因此不能刪除。  
  
 若要刪除屬性，請參閱[刪除屬性 &#40;Master Data Services&#41;](../delete-an-attribute-master-data-services.md)  
  
> [!TIP]  
>  變更有現有資料和相關實體之 MDS 屬性的資料類型，方法相當繁雜，特別是如果有相依於實體、已宣告的商務規則或訂閱檢視時。 最佳作法是一開始就讓資料類型具備足夠的彈性來保存必要值。 例如，字串一開始可能很小，不過在一段時間後可能變長，因此請考慮最嚴重的案例狀況。 額外的文字字串長度可能相當惱人 (例如，太寬的 GUI 文字方塊難以完整顯示在螢幕上)，因此請避免太長的字串長度。  
  
## <a name="see-also"></a>另請參閱  
 [Master Data Services &#40;的屬性&#41;](../attributes-master-data-services.md)   
 [建立模型 &#40;適用于 Excel 的 MDS 增益集&#41;](building-a-model-mds-add-in-for-excel.md)  
  
  
