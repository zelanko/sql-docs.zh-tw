---
title: 取代的資料表或具名的查詢中的資料來源檢視 (Analysis Services) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a171eafc35446f588d64c74457792912dcebe75a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34020805"
---
# <a name="replace-a-table-or-a-named-query-in-a-data-source-view-analysis-services"></a>取代資料來源檢視中的資料表或具名查詢 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在資料來源檢視設計工具中，您可以將資料來源檢視 (DSV) 中的資料表、檢視表或具名查詢取代為相同或不同資料來源中的不同資料表或檢視表，或是 DSV 中已定義的具名查詢。 當您取代資料表時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫或專案中有參考該資料表的所有其他物件仍可繼續參考該資料表，因為 DSV 中資料表的物件識別碼不變。 仍然相關的所有關聯性 (依據名稱和資料行類型比對) 都會保留下來。 相對而言，如果您先刪除，再加入資料表，則會失去參考和關聯性，而且必須重新建立。  
  
 若要將資料表取代成另一個資料表，您必須與專案模式下的資料來源檢視設計師的來源資料之間有使用中連接。  
  
 您最常將資料來源檢視中的資料表取代成資料來源中的另一個資料表。 不過，您也可以將具名查詢取代成資料表。 例如，您先前曾將資料表取代成具名查詢，而現在要還原為資料表。  
  
> [!IMPORTANT]  
>  如果您在資料來源中重新命名資料表，請遵循取代資料表的步驟，並在重新整理 DSV 之前，將重新命名的資料表指定 DSV 中的相對應資料表的來源。 完成取代及重新命名程序會在 DSV 中保留資料表、資料表的參考和資料表的關聯性。 否則，當您重新整理 DSV 時，資料來源中重新命名的資料表會被解譯為已刪除。 如需詳細資訊，請參閱[在資料來源檢視中重新整理結構描述 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/refresh-the-schema-in-a-data-source-view-analysis-services.md)。  
  
##  <a name="bkmk_nq"></a> 以具名查詢取代資料表  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，開啟含有您想在其中取代資料表或具名查詢之資料來源檢視的專案，或連接到包含此資料來源檢視的資料庫。  
  
2.  在方案總管中，展開 [資料來源檢視] 資料夾，然後按兩下資料來源檢視。  
  
3.  開啟 [建立具名查詢] 對話方塊。 在 [資料表] 或 [圖表] 窗格中，以滑鼠右鍵按一下您想要取代的資料表，並指向 [取代資料表]，然後按一下 [使用新具名查詢]。  
  
4.  在 [建立具名查詢] 對話方塊中，定義具名查詢，然後按一下 [確定]。  
  
5.  儲存已修改的資料來源檢視。  
  
## <a name="replace-a-table-or-named-query-with-a-table"></a>以資料表取代資料表或具名查詢  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，開啟含有您想在其中取代資料表或具名查詢之資料來源檢視的專案，或連接到包含此資料來源檢視的資料庫。  
  
2.  在方案總管中，展開 [資料來源檢視] 資料夾，然後按兩下資料來源檢視。  
  
3.  開啟 [使用其他資料表取代] 對話方塊。 在 [資料表] 或 [圖表] 窗格中，以滑鼠右鍵按一下您想要取代的資料表或具名查詢，並指向 [取代資料表]，然後按一下 [使用其他資料表]。  
  
4.  在 [使用其他資料表取代] 對話方塊中：  
  
    1.  在 [資料來源] 下拉式清單方塊中，選取想要的資料來源  
  
    2.  選取您想要用來取代資料表或具名查詢的資料表。  
  
5.  按一下 **[確定]**。  
  
6.  儲存已修改的資料來源檢視。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源檢視](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
