---
title: 刪除資料表（SSAS 表格式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: be4ed45f-fde3-466c-9869-49bd3ddb505e
author: minewiskan
ms.author: owend
ms.openlocfilehash: c72fa90426440c1be84318a15cf0d761ef16aca8
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939701"
---
# <a name="delete-a-table-ssas-tabular"></a>刪除資料表 (SSAS 表格式)
  在模型設計師中，您可以刪除模型工作空間資料庫中不再需要的資料表。 刪除資料表並不會影響原始來源資料，只會影響您匯入並在其中處理的資料。 您無法恢復資料表的刪除作業。  
  
### <a name="to-delete-a-table"></a>刪除資料表  
  
-   針對您要刪除的資料表，以滑鼠右鍵按一下模型設計師底部的索引標籤，然後按一下 [刪除]****。  
  
## <a name="considerations-when-deleting-tables"></a>刪除資料表時的考量  
  
-   當您刪除資料表時，資料表所在的整個索引標籤都會遭到刪除。  
  
-   如果有任何量值與該資料表相關聯，則也會刪除該量值的定義。  
  
-   如果您使用該資料表建立任何導出資料行，該資料表中的資料行也會遭到刪除；其他資料表中使用已刪除資料表之資料行的所有導出資料行則會顯示錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [資料表與資料行 &#40;SSAS 表格式&#41;](tables-and-columns-ssas-tabular.md)  
  
  
