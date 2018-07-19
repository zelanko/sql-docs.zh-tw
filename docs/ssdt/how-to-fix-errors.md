---
title: 如何：修正錯誤 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0d504e00-4ff0-4fdf-b874-85280bbd8668
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f4984e28ae3397b6296f8d1a39a6d32474b27f9c
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093893"
---
# <a name="how-to-fix-errors"></a>如何：修正錯誤
[錯誤清單] 窗格會顯示任何的部署或建置錯誤。 編輯資料庫實體及其定義時，Transact\-SQL 編輯器或資料表設計工具中的編輯所造成的語法或語意錯誤也會顯示在這個清單中。 當您跨不同索引標籤編輯指令碼時，[錯誤清單] 會以動態方式更新。 然後，您可以追蹤識別的錯誤以進行進一步疑難排解。  
  
> [!WARNING]  
> 下列程序使用在[連接的資料庫開發](../ssdt/connected-database-development.md)和[專案導向的離線資料庫開發](../ssdt/project-oriented-offline-database-development.md)小節中的程序所建立的實體。  
  
### <a name="to-fix-errors"></a>若要修正錯誤  
  
1.  以滑鼠右鍵按一下 [方案總管] 中的 [Product] 資料表 (Product.sql)，再選取 [檢視表設計工具]。  
  
2.  在設計工具的資料行格線中，以滑鼠右鍵按一下 [ShelflLife] 資料行，再選取 [刪除] 從資料表刪除這個資料行。  
  
3.  請注意，與下列訊息類似的警告與錯誤會立即顯示在畫面底部的 [錯誤清單] 中。  
  
**警告 SQL71502: 函數: [dbo].[GetProductsBySupplier] 包含物件無法解析的參考。可能是物件不存在，或是該參考因為參考到下列任一個物件而模稜兩可: [dbo].[Product].[p]::[ShelfLife] 或 [dbo].[Product].[ShelfLife]。錯誤 SQL71501: 檢查條件約束: [dbo].[CK_Product_ShelfLife] 有參考到物件 [dbo].[Product].[ShelfLife] 的無法解析參考。**  
  
4.  您可以用滑鼠右鍵按一下 [錯誤清單]，然後使用關聯式功能表排序結果，篩選要顯示的項目和每個項目要顯示的資訊欄。  
  
    按兩下第一個識別的警告，並跟著它找出產生警告的指令碼。 有問題的代碼區段會以反白顯示。 以我們所舉的例子來說，這是因為先前建立的資料表值函式中 `RETURN` 和 `SELECT` 陳述式都使用了 `ShelfLife` 資料行。  
  
5.  在 Transact\-SQL 編輯器中，從該函式移除 `ShelfLife`。  
  
6.  移除檢查條件約束，以類似的方式修正第二個錯誤。  
  
7.  請注意，在問題修正後，警告與錯誤隨即從 [錯誤清單] 中消失。  
  
## <a name="see-also"></a>另請參閱  
[使用 Transact-SQL 編輯器，編輯及執行指令碼](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)  
  
