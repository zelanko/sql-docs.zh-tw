---
title: 第 4 課：標記為日期資料表 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1ef1be7d87012b6ae1d1b69e3f2c92dccca86ac0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729194"
---
# <a name="lesson-4-mark-as-date-table"></a>第 4 課：標記為日期資料表
  在第 2 課：新增資料，匯入名為 DimDate 的維度資料表。 然後，您重新命名 DimDate 資料表中的，在第 3 課：重新命名資料行，只要，日期。 當模型中的此資料表已命名為 Date 時，也可以稱作「日期資料表」，並會在其中包含日期及時間資料。  
  
 每當您在計算中使用時間智慧函數時，就像您稍後建立量值時一樣，必須指定日期資料表屬性，其中包含「日期資料表」，以及該資料表中的唯一識別碼「日期資料行」。 接著您就可以在其他資料表與此 Date 資料表之間建立有效的關聯性；這對於使用 DAX 時間智慧函數進行計算為必要步驟。  
  
 在這一課，您將標記所匯入並重新命名的 Date 資料表為「日期資料表」，而 Date 資料行 (包含在 Date 資料表中) 則會標記為「日期資料行」(唯一識別碼)。 日期可以取得有點令人困惑的名稱，但您的所有使用很快就會都了解這個概念。  
  
 估計的時間才能完成這一課：**3 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
 本主題是表格式模型教學課程的一部分，必須依序完成。 執行工作之前在這一課，您應已完成上一課：[第 3 課：重新命名資料行](rename-columns.md)。  
  
### <a name="to-set-mark-as-date-table"></a>設定標記為日期資料表  
  
1.  在模型設計師中，按一下 [Date] 資料表 (索引標籤)。  
  
2.  依序按一下 [資料表] 功能表、[日期] 和 [標記為日期資料表]。  
  
3.  在 [標記為日期資料表] 對話方塊的 [日期] 清單方塊中，選取 [日期] 資料行當作唯一識別碼。  
  
## <a name="next-steps"></a>後續步驟  
 若要繼續本教學課程，請移至下一課：[第 5 課：建立關聯性](lesson-4-create-relationships.md)。  
  
  
