---
title: "從採礦模型鑽研到案例資料 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- drillthrough [Analysis Services]
ms.assetid: b4d3f350-e543-4ea9-b3a2-b4f7c0a9ae27
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 849c244bdfb40770d8038a78a430faa7ff26b6b8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="drill-through-to-case-data-from-a-mining-model"></a>鑽研採礦模型的案例資料
  如果採礦模型已經設定為讓您鑽研模型案例，當您瀏覽此模型時，可以擷取有關用來建立模型之案例的詳細資訊。 此外，如果基礎採礦結構已經設定為允許鑽研結構案例，而且您擁有適當的權限，就可以從採礦結構傳回資訊。 這可能包括沒有包含在採礦模型中的資料行。  
  
 如果採礦結構不允許您鑽研基礎資料，但是採礦模型允許，您就可以檢視模型案例的資訊，但無法檢視採礦結構的資訊。  
  
> [!NOTE]  
>  您可以將 **AllowDrillthrough** 屬性設定為 **True**來加入鑽研現有採礦模型的功能。 不過，在您啟用鑽研之後，必須先重新處理此模型，然後才能查看案例資料。 如需詳細資訊，請參閱 [針對採礦模型啟用鑽研](../../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)。  
  
 根據您所使用的檢視器類型，可以透過下列方式來選取鑽研的節點：  
  
|檢視器名稱|窗格或索引標籤名稱|選取節點|  
|-----------------|----------------------|-----------------|  
|**Microsoft 樹狀檢視器**|**決策樹** 索引標籤|按一下樹狀節點。<br /><br /> **注意**：請避免在 [全部] 節點上使用鑽研，因為它可能需要很長的時間才能傳回結果。|  
|**Microsoft 叢集檢視器**|**群集圖表**|按一下叢集節點。|  
|**Microsoft 叢集檢視器**|**叢集設定檔**|按一下群集資料行中的任何位置。|  
|**Microsoft 關聯檢視器**|**規則** 索引標籤|按一下包含一組規則的資料列。|  
|**Microsoft 關聯檢視器**|**項目集** 索引標籤|按一下包含項目集的資料列。|  
|**Microsoft 時序群集檢視器**|**規則** 索引標籤|按一下包含一組規則的資料列。|  
|**Microsoft 時序群集檢視器**|**項目集** 索引標籤|按一下包含項目集的資料列。|  
  
> [!NOTE]  
>  有些模型無法使用鑽研。 使用鑽研的能力取決於建立模型所使用的演算法。 如需支援鑽研之採礦模型類型的清單，請參閱 [鑽研查詢 &#40;資料採礦&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)來加入鑽研現有採礦模型的功能。  
  
### <a name="to-view-drillthrough-data-from-a-mining-model"></a>若要檢視採礦模型中的鑽研資料  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需之採礦模型的採礦結構。  
  
2.  在資料採礦設計師中，按一下 **[採礦模型檢視器]** 索引標籤。  
  
3.  從 [採礦模型] 下拉式清單中選取模型。  
  
4.  從 [檢視器] 下拉式清單中選取一個檢視器，然後以滑鼠右鍵按一下特定的節點。  
  
5.  選取 [鑽研]，然後選取 [僅模型資料行] 或 [模型和結構資料行]，即可開啟 [鑽研] 視窗。  
  
6.  若要將資料複製到剪貼簿，請以滑鼠右鍵按一下資料表中的任何資料列，然後選取 [全部複製]。  
  
## <a name="see-also"></a>另請參閱  
 [鑽研查詢 &#40;資料採礦&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
  

