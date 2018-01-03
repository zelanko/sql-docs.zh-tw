---
title: "以多個資料行聯結資料表 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multiple column joins
- joins [SQL Server], multiple columns
ms.assetid: 56a158bc-a42a-4b78-baad-4721d2d22cd3
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bfe676ff39f2ce59cd9c9b39915ff6393d5f9b6a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="join-tables-on-multiple-columns-visual-database-tools"></a>以多個資料行聯結資料表 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 可以聯結具有多重資料行的資料表。 也就是說，可以建立查詢，使其找出兩個資料表中滿足多重條件的資料列。 如果資料庫包含使某資料表中多重外部索引鍵資料行符合另一個資料表中多重資料行主索引鍵的關聯性，則可以使用此關聯性來建立多重資料行聯結。 如需詳細資料，請參閱[自動聯結資料表 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md)。  
  
即使資料庫不包含多重資料行外部索引鍵關聯性，也可以手動建立聯結。  
  
### <a name="to-manually-create-a-multicolumn-join"></a>若要手動建立多重資料行聯結  
  
1.  將您要聯結的資料表新增到 [圖表窗格](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) 中。  
  
2.  將第一個資料表視窗中的第一個聯結資料行，拖放至第二個資料表視窗中的相關資料行。 不可讓聯結以 text、ntext 或 image 資料行為基礎。  
  
    > [!NOTE]  
    > 一般來說，聯結資料行必須具有相同的 (或相容的) 資料類型。 例如，如果第一個資料表的聯結資料行為日期，就必須關聯至第二個資料表的日期資料行。 另一方面，如果第一個聯結資料行為整數，則關聯的聯結資料行也必須為整數資料類型，但其大小可有所不同。 然而，可能會發生隱含的資料類型轉換聯結似乎不相容的資料行的情形。  
    >   
    > [查詢和檢視設計工具](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 不會檢查您建立聯結時所使用的資料行資料類型，但當您執行查詢時，若資料類型不相容，資料庫便會顯示錯誤。  
  
3.  將第一個資料表視窗中的第二個聯結資料行，拖放至第二個資料表視窗中的相關資料行。  
  
4.  對兩個資料表中其他的聯結資料行重複步驟 3。  
  
5.  執行查詢。  
  
## <a name="see-also"></a>另請參閱  
[使用聯結查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
