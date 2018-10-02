---
title: 如何：使用資料表設計工具管理資料表和關聯性 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.design.table.columnspecification.index.dialog
- sql.data.tools.design.table.columnsgrid.view
- sql.data.tools.design.table.scriptpanel
ms.assetid: 322a2903-d7a6-4f52-9048-1bd413b4c799
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6a312fbcfe6cfb25f612bb095bcff70656009a11
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47652868"
---
# <a name="how-to-use-the-table-designer-to-manage-tables-and-relationships"></a>如何：使用資料表設計工具管理資料表和關聯性
資料表設計工具與 Transact\-SQL 編輯器一起為 SQL Server 資料庫提供用於建立及編輯資料表結構 (包括資料表特定的程式設計物件) 的視覺效果。  為連接的資料庫或專案建立新資料表，或是在 [SQL Server 物件總管] 或 [方案總管] 中按兩下資料表加以編輯時，就會啟動資料表設計工具。  
  
這個設計工具由資料行格線、指令碼窗格和內容窗格組成。 資料行格線會列出資料表中的所有資料行。 您可以加入、編輯和刪除此格線中的資料行。  內容窗格提供資料表定義 (索引鍵、索引、條件約束、觸發程序等等) 的邏輯檢視，並讓您選取要反白顯示與個別資料行關聯性的物件。 您也可以將新物件加入至這個窗格中的資料表，並在 [屬性] 方格中編輯所選取物件的屬性。 指令碼窗格會顯示資料表結構的定義，並在內容窗格或資料行格線中反白顯示所選物件的指令碼。 您可以在檢視中使用資料行格線和內容窗格並存編輯指令碼。 任何三個窗格的任何變更都會將立即傳播到其他兩個窗格。  
  
> [!WARNING]  
> 下列程序使用在[連接的資料庫開發](../ssdt/connected-database-development.md)和[專案導向的離線資料庫開發](../ssdt/project-oriented-offline-database-development.md)小節中的程序所建立的實體。  
  
### <a name="to-create-a-new-table"></a>若要建立新資料表  
  
1.  開啟先前的程序中使用的 TradeDev 專案。  
  
2.  在 [方案總管] 中展開 [dbo] 資料夾，以滑鼠右鍵按一下 [資料表] 資料夾，再依序選取 [加入] 和 [資料表]。  
  
3.  將新資料表命名為 **Shipper**，然後按一下 [加入]。  
  
4.  資料表設計工具隨即開啟。 在資料行格線中，使用名稱 **ShipperName** 和資料類型 **int** 將新資料行加入至資料表。  
  
5.  請注意，您還可以在 [屬性] 視窗中編輯資料行的屬性。 按一下 [ShipperName] 資料行，然後在 [屬性] 視窗中將這個資料行的 [DataType] 變更為 **nvarchar**，並將 [length] 變更為 **128**。 請注意，將焦點從欄位移開時，這個設計工具的指令碼窗格和資料行格線會自動更新以反映變更。  
  
### <a name="to-create-a-new-foreign-key-constraint"></a>若要建立新的外部索引鍵條件約束  
  
1.  在這個設計工具的內容窗格中，以滑鼠右鍵按一下 [外部索引鍵]，再選取 [加入新的外部索引鍵]。  
  
2.  請注意，節點計數會自動遞增 1。 按 ENTER 接受條件約束的預設名稱。  
  
3.  以下列內容取代指令碼窗格中之條件約束的預設定義。  
  
    ```  
    CONSTRAINT [FK_Shipper_Products] FOREIGN KEY ([Id]) REFERENCES [dbo].[Products]([Id])  
    ```  
  
    請注意，為離線專案建立及編輯資料庫實體的效果與執行連接的資料庫工作完全一樣。  
  
## <a name="see-also"></a>另請參閱  
[如何：使用資料表設計工具建立資料庫物件](../ssdt/how-to-create-database-objects-using-table-designer.md)  
  
