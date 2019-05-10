---
title: 變更屬性類型 (適用於 Excel 的 MDS 增益集) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9d3001d9-8d0f-4e4a-8e04-4f666bf0df69
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ecdbff5b071ae82fe8bd8322c1ef9d46f153b0cc
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65488899"
---
# <a name="change-the-attribute-type-mds-add-in-for-excel"></a>變更屬性類型 (適用於 Excel 的 MDS 增益集)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，當資料類型或是允許的字元數目不正確時，管理員可以變更屬性類型。  
  
 如果您想要變更屬性類型來建立受條件約束的清單 (網域屬性)，請參閱[建立網域屬性 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)。  
  
> [!NOTE]  
>  您不能更新 **Name** 或 **Code** 資料行的類型或長度。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 [系統管理] 和總管功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](../../master-data-services/administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
-   必須有現有的模型、實體和屬性存在。  
  
### <a name="to-change-the-attribute-type"></a>若要變更屬性類型  
  
1.  在 Excel 中，載入包含您想要變更之資料行 (屬性) 的實體。 如需詳細資訊，請參閱 [Export Data to Excel from Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)(將資料從 Master Data Services 匯入 Excel)。  
  
2.  在您想要變更的資料行中按一下任何資料格。  
  
3.  在 [建立模型] 群組中，按一下 [屬性內容]。  
  
4.  在 [屬性內容] 對話方塊中，視需要更新設定。  
  
5.  按一下 [確定] 。  
  
## <a name="what-happens-when-you-change-the-attribute-type"></a>當您變更屬性類型時會發生什麼情況？  
 如果對屬性具有任何相依性 (例如，有任何 MDS 商務規則或衍生階層參考屬性)，則無法變更屬性的資料類型。 您收到一則錯誤，指出無法修改屬性類型，因為它是由物件所參考。  
  
 如果屬性值的資料類型轉換期間發生任何錯誤，則 MDS 會執行下列動作。  
  
-   變更屬性的資料類型。  
  
-   產生具有後置詞 "_old" 且包含先前值的屬性複本。 這稱為已被取代的屬性。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;Master Data Services&#41;](../../master-data-services/attributes-master-data-services.md)   
 [建立模型 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/building-a-model-mds-add-in-for-excel.md)  
  
  
