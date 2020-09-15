---
description: 資料表和資料行對話方塊 (Visual Database Tools)
title: 資料表和資料行對話方塊
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.tablesandcolumns
ms.assetid: 8cf27be1-e66d-4735-a428-9ab4b33af4f5
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 8cc13808b01f33c623304f46efcde3e7e063f713
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88369364"
---
# <a name="tables-and-columns-dialog-box-visual-database-tools"></a>資料表和資料行對話方塊 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
使用此對話方塊將一個資料表中的主索引鍵對應至另一個資料表中的外部索引鍵。 若要存取此對話方塊，請從 [資料表設計工具]**** 功能表按一下 [關聯性]****。 在 [外部索引鍵關聯性]**** 對話方塊中，按一下 [資料表及資料行規格]**** 欄位，然後按一下屬性右邊的省略符號 ([...]****)。  
  
> [!NOTE]  
> 如果資料表是要發佈以進行複寫，則必須使用 Transact-SQL 陳述式 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 或 SQL Server 管理物件 (SMO) 變更結構描述。 使用 [資料表設計工具] 或 [資料庫圖表設計工具] 變更結構描述時，會嘗試卸除並重新建立資料表。 您無法卸除已發行的物件，因此結構描述變更將會失敗。  
  
## <a name="options"></a>選項  
**關聯性名稱**  
顯示關聯性的名稱。  
  
**主索引鍵資料表**  
列出資料庫中的資料表。 選擇將位在關聯性主索引鍵端的資料表。  
  
**外部索引鍵資料表**  
顯示位在關聯性外部索引鍵端的資料表。 這是目前在 [資料表設計師] 中選取的資料表。  
  
**主索引鍵資料表底下方格**  
列出在 [主索引鍵資料表]**** 清單中所選取資料表的資料行。 輸入提供該資料表之主索引鍵的資料行。  
  
**外部索引鍵資料表底下方格**  
列出在 [外部索引鍵資料表]**** 清單中所選取資料表的資料行。 輸入外部索引鍵資料表的外部索引鍵資料行，該資料行對應至主索引鍵資料行。  
  
> [!NOTE]  
> 為外部索引鍵選擇的資料行，必須與對應到的主索引鍵資料行具有相同的資料類型。 每個索引鍵中的資列行數目必須相等。 例如，如果位在關聯性主索引鍵端的資料表之主索引鍵是由兩個資料行所組成，這兩個資料行的每一個都必須與關聯性外部索引鍵端資料表中的一個資料行相符。  
  
## <a name="see-also"></a>另請參閱  
[如何：建立資料表之間的關聯性(https://msdn.microsoft.com/867a54b8-5be4-46e6-9702-49ae6dabf67c)  
  
