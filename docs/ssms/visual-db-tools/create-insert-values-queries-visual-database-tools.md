---
title: 建立插入值查詢 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting values
- queries [SQL Server], types
- adding values
- row additions [SQL Server], Insert Values query
- inserting rows
- Insert Values query
- adding rows
- table values [SQL Server]
ms.assetid: 2d4b2f6d-cc09-434b-8a0e-ccce40628064
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5f1fb77b9664de6806a5dd49420267919be28c59
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65105885"
---
# <a name="create-insert-values-queries-visual-database-tools"></a>建立插入值查詢 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
您可使用 [插入值] 查詢在目前的資料表中建立新資料列。 當建立 [插入值] 查詢時，您指定：  
  
-   要加入資料列的資料庫資料表。  
  
-   要加入內容的資料行。  
  
-   用來插入至個別資料行的值或運算式。  
  
例如，下列查詢會將資料列加入至 `titles` 資料表，同時指定標題，類型，發行者和價格的值：  
  
```  
INSERT INTO titles  
         (title_id, title, type, pub_id, price)  
VALUES   ('BU9876', 'Creating Web Pages', 'business', '1389', '29.99')  
```  
  
當建立 [插入值] 查詢時，[準則] 窗格會變更以反映插入新資料列僅只使用的選項：資料行名稱與要插入的值。  
  
> [!CAUTION]  
> [插入值] 查詢執行的動作無法恢復。 為安全起見，在執行查詢前請先備份資料。  
  
### <a name="to-create-an-insert-values-query"></a>若要建立 [插入值] 查詢  
  
1.  將要更新的資料表加入至 [圖表] 窗格。  
  
2.  在 [查詢設計工具]  功能表中指向 [變更類型]  ，然後按一下 [插入值]  。  
  
    > [!NOTE]  
    > 當啟動 [插入值] 查詢時，[圖表] 窗格中若顯示一個以上之資料表，[查詢和檢視表設計工具] 會顯示[選擇插入值的目標資料表對話方塊](../../ssms/visual-db-tools/choose-target-table-for-insert-values-dialog-box-visual-database-tools.md)，詢問要更新的資料表名稱。  
  
3.  在 [圖表] 窗格中，按一下要提供新值之各資料行的核取方塊。 這些資料行將顯示在 [準則] 窗格中。 只有加入查詢中的資料行才會更新。  
  
4.  在 [準則] 窗格之 [新值]  資料行中，輸入資料行的新值。 您可輸入常值、資料行名稱或運算式。 該值必須符合 (或相容於) 正在更新之資料行的資料類型。  
  
    > [!CAUTION]  
    > 查詢和檢視設計師不會檢查值是否符合要插入之資料行的長度。 如果提供的值太長，它可能會無預警地被截斷。 例如，如果 `name` 資料行的長度是 20 個字元，但是您指定了 25 個字元的插入值，最後 5 個字元可能會被截斷。  
  
當執行 [插入值] 查詢時， [結果窗格](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)不會報告結果。 而是出現訊息指出已經變更了多少資料列。  
  
## <a name="see-also"></a>另請參閱  
[支援的查詢類型 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[使用查詢執行基本作業 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
