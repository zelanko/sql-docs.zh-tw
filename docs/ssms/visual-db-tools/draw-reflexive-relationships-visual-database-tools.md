---
title: 繪製自反關聯性 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- drawing reflexive relationships
- reflexive relationships
- database diagrams [SQL Server], relationships
ms.assetid: e218363f-faec-46d5-9904-a537fbcc994d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: be3abc83b3084626f714efa6628fc7cfe1547867
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105305"
---
# <a name="draw-reflexive-relationships-visual-database-tools"></a>繪製自反關聯性 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
您可建立自反關聯性 (Reflexive Relationship)，將資料表中的一或多個資料行與相同資料表中的其他資料行連結。 例如，假設 `employee` 資料表包含 `emp_id` 資料行和 `mgr_id` 資料行。 由於每位經理同時兼具員工的身分，您可繪製一條從資料表至其本身的關聯線，將這兩個資料行相關聯。 此關聯性可確保每個加入資料表的經理識別碼，都與現有員工識別碼相符。  
  
在建立關聯性之前，必須先為您的資料表定義主索引鍵或唯一的條件約束。 然後，將主索引鍵資料行關聯至相符的資料行。 建立關聯性之後，相符的資料行會成為資料表的外部索引鍵。  
  
### <a name="to-draw-a-reflexive-relationship"></a>若要繪製自反關聯性  
  
1.  在資料庫圖表中，在要關聯至其他資料行的資料庫資料行上按一下資料列選取器，並將指標拖曳至資料表外部，直到線條顯示為止。  
  
2.  將線條拖曳回選取的資料表。  
  
3.  放開滑鼠按鈕。 隨即出現 [資料表和資料行] 對話方塊。  
  
4.  選取要用來形成關聯性的外部索引鍵資料行及主索引鍵資料表與資料行。  
  
5.  選擇兩次 [確定] 以建立關聯性。  
  
當您對資料表執行查詢時，可使用自反關聯性來建立自我聯結 (Self-Join)。 如需使用聯結查詢資料表的相關資訊，請參閱 [使用聯結查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)。  
  
## <a name="see-also"></a>另請參閱  
[使用聯結查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
