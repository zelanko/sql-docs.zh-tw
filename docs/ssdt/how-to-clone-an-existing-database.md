---
title: 如何：複製現有的資料庫 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: aad3594a-11cf-4e68-a622-071a93d43875
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 683d8f082a41b328f9cf86134cee0440e2ca3e4a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818753"
---
# <a name="how-to-clone-an-existing-database"></a>如何：複製現有的資料庫
這個工作將使用一些您在先前的程序中所學到的步驟，建立新的資料庫並移植現有的資料。 此外，它還使用[如何：使用結構描述比較，比較不同的資料庫定義](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)中所述的步驟，來同步處理來源和專案資料庫的結構描述。  
  
利用這些步驟，您可以輕鬆地從生產資料庫建立具有相同結構描述和資料的開發或測試資料庫。 然後，您可以繼續在連線模式下開發測試資料庫，或是建立資料庫專案供離線開發和測試使用，所有工作都不必中斷生產資料庫的作業。  
  
> [!WARNING]  
> 下列程序將使用先前在[連接的資料庫開發](../ssdt/connected-database-development.md)小節的程序中所建立的實體。  
  
### <a name="to-create-a-development-database"></a>若要建立開發資料庫  
  
1.  在 [SQL Server 物件總管] 中，展開 [SQL Server] 節點底下連接的伺服器執行個體。  
  
2.  以滑鼠右鍵按一下 [資料庫] 節點，再選取 [加入新的資料庫]。  
  
3.  將新的資料庫重新命名為 **TradeDev**。  
  
4.  以滑鼠右鍵按一下 [SQL Server 物件總管] 中的 [Trade] 資料庫，再選取 [結構描述比較]。 遵循[如何：使用結構描述比較，比較不同的資料庫定義](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)主題中的步驟，選擇原始的 **Trade** 資料庫做為來源，新的 **TradeDev** 資料庫做為目標。 這會以 **Trade** 的結構描述來更新 **TradeDev**。  
  
### <a name="to-replicate-data"></a>若要複寫資料  
  
1.  上一個步驟只複製生產資料庫的結構描述至開發資料庫。 在這個程序中，您將複製生產資料至開發資料庫。  
  
    以滑鼠右鍵按一下 [Trade] 資料庫中的 [Suppliers] 資料表，再選取 [檢視資料]。 資料編輯器隨即開啟。  
  
2.  按一下工具列上 [最大資料列] 旁邊的 [指令碼] 按鈕。  
  
3.  當指令碼視窗開啟時，請確認在 Transact\-SQL 指令碼窗格下方的狀態列中顯示「已連接」。 如果顯示「已中斷連接」，請按一下 [連接] 按鈕 (工具列上最左邊的按鈕)，然後輸入您的伺服器資訊和認證。  
  
4.  在 [連接]/[中斷連接] 按鈕旁邊的 [資料庫] 下拉式功能表中，選取 [TradeDev]。 這類似於 Transact\-SQL`USE` 陳述式，而且將確保程式碼編輯器中的指令碼的執行對象會是 **TradeDev** 資料庫。  
  
5.  按一下 [執行查詢] 按鈕執行 `INSERT` 陳述式。 這會將 `Suppliers` 資料庫的 `Trade` 資料表中的所有資料列插入 `Suppliers` 資料庫的 `TradeDev` 資料表。  
  
6.  為 `Trade` 資料庫中的所有資料表重複前面的步驟，讓它們全部都複寫到 `TradeDev` 資料庫。  
  
7.  使用資料編輯器，確認新的 `TradeDev` 資料庫中的所有資料表全部都已填入。  
  
## <a name="see-also"></a>另請參閱  
[如何：使用結構描述比較，比較不同的資料庫定義](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)  
  
