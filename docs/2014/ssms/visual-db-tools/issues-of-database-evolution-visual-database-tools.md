---
title: 資料庫演進問題 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], multuser database changes
- database evolution [SQL Server]
ms.assetid: 1ed6ae10-d212-4ec2-8569-1b94ab1cba6d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d3a1f10ae77061983a5cf64ddd5a3462bb4be49b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63035587"
---
# <a name="issues-of-database-evolution-visual-database-tools"></a>資料庫演進問題 (Visual Database Tools)
  如果您變更了某部署資料庫的結構，您必須特別注意您的變更是否與現有資料和資料庫結構相容。 進行下列修改時您可能必須採取特殊步驟：  
  
-   **新增條件約束**：如果您新增某樣條件約束，該資料庫可能已含有無法滿足該條件約束的資料。 當您儲存新的條件約束時，[儲存後告知對話方塊 &#40;Visual Database Tools&#41;](visual-database-tools.md) 將通知您資料庫伺服器無法建立該條件約束。 若要強制資料庫接受新的條件約束，您可以清除 [建立時立即檢查現有資料]  核取方塊。  
  
-   **新增關聯性**：如果新增關聯性，該資料庫可能已含有外部索引鍵資料表資料列，該資料列在主索引資料列中並未有對應的資料列。 也就是說，現有資料可能無法滿足參考完整性。 當您儲存新的關聯性時，[儲存後告知對話方塊 &#40;Visual Database Tools&#41;](visual-database-tools.md) 將通知您資料庫伺服器無法儲存修改過的外部索引鍵資料表。 若要強制資料庫接受修改，您可以清除 [建立時立即檢查現有資料]  核取方塊。  
  
-   **修改提供索引檢視的資料表**：如果您修改提供 Microsoft SQL Server 索引檢視的資料表，將會遺失該檢視上的所有索引。 如需重建索引的詳細資訊，請參閱《SQL Server 線上叢書》。  
  
-   **刪除物件** ：如果您刪除資料行、資料表或檢視之類的物件，請先進行檢查，確認資料庫中並無其他物件參考該物件。  
  
 不論您如何變更資料庫設計，您應該保留一份變更記錄。 方法之一就是保留您對實際執行資料庫進行的所有 SQL 指令碼修改。  
  
## <a name="see-also"></a>另請參閱  
 [Unique 條件約束和 Check 條件約束](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [多使用者環境 &#40;Visual Database Tools&#41;](multiuser-environments-visual-database-tools.md)  
  
  
