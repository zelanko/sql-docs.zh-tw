---
description: 資料庫演進問題 (Visual Database Tools)
title: 資料庫演進問題
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], multuser database changes
- database evolution [SQL Server]
ms.assetid: 1ed6ae10-d212-4ec2-8569-1b94ab1cba6d
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 88f2c0cff6bd33bf5327c7c919370015873700ec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88314624"
---
# <a name="issues-of-database-evolution-visual-database-tools"></a>資料庫演進問題 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
如果您變更了某部署資料庫的結構，您必須特別注意您的變更是否與現有資料和資料庫結構相容。 進行下列修改時您可能必須採取特殊步驟：  
  
-   **新增條件約束**：如果您新增某樣條件約束，該資料庫可能已含有無法滿足該條件約束的資料。 當您儲存新的條件約束時，[儲存後告知對話方塊 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/post-save-notifications-dialog-box-visual-database-tools.md) 將通知您資料庫伺服器無法建立該條件約束。 若要強制資料庫接受新的條件約束，您可以清除 [建立時立即檢查現有資料]**** 核取方塊。  
  
-   **新增關聯性**：如果新增關聯性，該資料庫可能已含有外部索引鍵資料表資料列，該資料列在主索引資料列中並未有對應的資料列。 也就是說，現有資料可能無法滿足參考完整性。 當您儲存新的關聯性時，[儲存後告知對話方塊 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/post-save-notifications-dialog-box-visual-database-tools.md) 將通知您資料庫伺服器無法儲存修改過的外部索引鍵資料表。 若要強制資料庫接受修改，您可以清除 [建立時立即檢查現有資料]**** 核取方塊。  
  
-   **修改提供索引檢視的資料表**：如果您修改提供 Microsoft SQL Server 索引檢視的資料表，將會遺失該檢視上的所有索引。 如需重建索引的詳細資訊，請參閱《SQL Server 線上叢書》。  
  
-   **刪除物件** ：如果您刪除資料行、資料表或檢視之類的物件，請先進行檢查，確認資料庫中並無其他物件參考該物件。  
  
不論您如何變更資料庫設計，您應該保留一份變更記錄。 方法之一就是保留您對實際執行資料庫進行的所有 SQL 指令碼修改。  
  
## <a name="see-also"></a>另請參閱  
[使用條件約束](https://msdn.microsoft.com/637098af-2567-48f8-90f4-b41df059833e)  
[多使用者環境 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/multiuser-environments-visual-database-tools.md)  
  
