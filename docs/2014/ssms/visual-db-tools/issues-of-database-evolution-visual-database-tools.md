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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63035587"
---
# <a name="issues-of-database-evolution-visual-database-tools"></a>資料庫演進問題 (Visual Database Tools)
  如果您變更了某部署資料庫的結構，您必須特別注意您的變更是否與現有資料和資料庫結構相容。 進行下列修改時您可能必須採取特殊步驟：  
  
-   **加入條件約束**如果您加入條件約束，則資料庫可能已經包含無法滿足此限制的資料。 當您儲存新的條件約束時，[儲存後告知對話方塊 &#40;Visual Database Tools&#41;](visual-database-tools.md) 將通知您資料庫伺服器無法建立該條件約束。 若要強制資料庫接受新的條件約束，您可以清除 [建立時立即檢查現有資料]**** 核取方塊。  
  
-   **加入關聯**性如果您加入關聯性，該資料庫可能已經包含外鍵資料表的資料列，但在主鍵資料表中沒有對應的資料列。 也就是說，現有資料可能無法滿足參考完整性。 當您儲存新的關聯性時，[儲存後告知對話方塊 &#40;Visual Database Tools&#41;](visual-database-tools.md) 將通知您資料庫伺服器無法儲存修改過的外部索引鍵資料表。 若要強制資料庫接受修改，您可以清除 [建立時立即檢查現有資料]**** 核取方塊。  
  
-   **修改參與索引視圖的資料表**如果您修改的資料表會參與 Microsoft SQL Server 索引視圖，則此視圖上的索引將會遺失。 如需重建索引的詳細資訊，請參閱《SQL Server 線上叢書》。  
  
-   **刪除物件**如果您刪除物件（例如資料行、資料表或視圖），請先檢查以確定資料庫中的另一個物件不會參考該物件。  
  
 不論您如何變更資料庫設計，您應該保留一份變更記錄。 方法之一就是保留您對實際執行資料庫進行的所有 SQL 指令碼修改。  
  
## <a name="see-also"></a>另請參閱  
 [Unique 條件約束和 Check 條件約束](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [多使用者環境 &#40;Visual Database Tools&#41;](multiuser-environments-visual-database-tools.md)  
  
  
