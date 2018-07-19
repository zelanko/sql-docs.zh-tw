---
title: 協調多位使用者所做的變更 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- table modifications [SQL Server], multiple users
- reconciling changes made by multiple users
- modifications made by multiple users
ms.assetid: fc7ed4f2-ad3d-47fc-a3ef-51e5bb069ef0
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 70dd406f128f9df1cb36ac6c4ddcd0dd18b446aa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33051775"
---
# <a name="reconcile-changes-made-by-multiple-users-visual-database-tools"></a>協調多位使用者所做的變更 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
在多位使用者環境中，可以同時讓多位使用者修改相同的物件。 這樣的情況會發生在當您使用資料表或資料庫圖表設計工具設計物件的結構時，或是發生在 [查詢和檢視設計師] 的 [結果] 窗格中的值。 這樣會產生您需要解決的衝突。  
  
## <a name="conflicts-in-the-table-or-database-diagram-designers"></a>在資料表或資料庫圖表設計工具中的衝突  
例如，另外一位使用者可能會刪除或重新命名您正在 [資料表設計工具] 中使用的相同或相關資料表。 當您嘗試儲存資料表時， [偵測到資料庫變更對話方塊 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/database-changes-detected-dialog-box-visual-database-tools.md) 會通知您資料庫已經在您開啟資料表之後經過更新。  
  
這個對話方塊將同時顯示資料庫物件清單，其中包含儲存資料表時將會受到影響的所有物件。 這個時候您可以採取下列行動：  
  
-   選擇 [是] 可儲存資料表，並且可使用清單中的所有變更更新資料庫。  
  
    這個動作會影響共用相同資料庫物件的資料表。 例如，假設您編輯 `titleauthors` 資料表中的 `au_id` 資料行，而另一位使用者正在使用與 `titleauthors` 資料表 `au_id` 資料行相關的 `authors` 資料表。 如果您儲存您的資料表將會影響其他使用者的資料表。 同樣的，假設其他使用者在 `qty` 資料表中定義了一個 `sales` 資料行的檢查條件約束。 如果您刪除 `qty` 資料行並儲存 `sales` 資料表，則會影響其他使用者的檢查條件約束。  
  
-   選擇 [否] 會取消儲存動作。  
  
    您可關閉資料表而不加以儲存。 當您重新開啟資料表，會與在資料庫中的相符。  
  
-   選擇 [儲存為文字檔] 可儲存變更清單。  
  
    您可以將 [偵測到資料庫變更] 對話方塊中所示的資料庫變更清單儲存為文字檔，以便您了解其他使用者變更的原因。 例如，如果其他使用者編輯您標示為刪除的資料表，您可能想要研究是否應在更新資料庫之前刪除該資料表。  
  
## <a name="conflicts-in-the-query-and-view-designer"></a>在 [查詢和檢視設計師] 中的衝突  
如果您執行查詢或傳回檢視的結果，資料會顯示在 [結果窗格](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)中。 多位使用者可以在同時使用相同的資料集，但這樣可能會產生衝突。  
  
例如，假設您和您的同事分別執行一個查詢，以顯示 `titleauthors` 資料表的所有資料。 您的同事將所回傳的第一筆記錄中的名字 Barb 變更為 Barbara。 在這個時候資料庫中這個資料欄位已經是 Barbara，但您的結果集還是顯示 Barb。 現在您輸入 Barbara 然後按下該資料列。 您會收到詢問您要如何解決衝突的訊息。  
  
-   按一下 [是] 可使用您的變更更新資料庫。  
  
    這會覆寫您同事的變更。  
  
-   按一下 [否] 可以將您的結果集更新為資料庫中目前的狀態。  
  
    這會使用您同事的變更覆寫您的變更。  
  
-   按一下 [取消] 可繼續編輯，而不會解決衝突。  
  
    在這種狀況下，您無法變更資料庫。  
  
## <a name="see-also"></a>另請參閱  
[偵測到資料庫變更對話方塊 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/database-changes-detected-dialog-box-visual-database-tools.md)  
  
