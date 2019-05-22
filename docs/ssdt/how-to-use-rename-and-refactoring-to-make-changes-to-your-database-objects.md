---
title: 如何：使用重新命名與重構變更資料庫物件 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.dbrefactoring.previewdialog
- sql.data.tools.editor.howto.refactoring
- sql.data.tools.dbrefactoring.renamedialog
- sql.data.tools.dbrefactoring.moveschemadialog
- sql.data.tools.dbrefactoring.renameserverdatabasedialog
ms.assetid: f35520e6-8e6e-47b1-87a3-22c0cf2cabdb
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a9da86a5e15f1b683a0e7c040cd4e6d906d54f47
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65090089"
---
# <a name="how-to-use-rename-and-refactoring-to-make-changes-to-your-database-objects"></a>如何：使用重新命名和重構，變更資料庫物件
Transact\-SQL 編輯器的 [重構] 關聯式功能表可讓您重新命名物件或將物件移至其他結構描述，並且在認可變更之前預覽所有受影響的區域。 您也可以使用 [重構] 功能表，在資料庫專案中完整限定資料庫物件的所有參考，或是擴充 `SELECT` 陳述式內的任何萬用字元。  
  
> [!NOTE]  
> 下列程序利用先前在[連接的資料庫開發](../ssdt/connected-database-development.md)和[專案導向的離線資料庫開發](../ssdt/project-oriented-offline-database-development.md)小節中的程序所建立的實體。  
  
### <a name="to-rename-a-type"></a>若要重新命名類型  
  
1.  以滑鼠右鍵按一下 [方案總管] 中的 [Products] 資料表 (Products.sql)，再選取 [檢視程式碼]，在 Transact\-SQL 編輯器中開啟指令碼。  
  
2.  以滑鼠右鍵按一下指令碼中的 `[Products]`，再依序選取 [重構] 和 [重新命名]。  
  
3.  在 [新名稱] 欄位中將它變更為 **Product**。 讓 [預覽變更] 選項處於選取狀態，然後按一下 [確定]。  
  
4.  在下一個畫面中，您便可以預覽即將受到這個重新命名作業影響的指令碼清單。 特別是，所有參考 `Products` 的地方都會以反白顯示。 這非常類似於先前的程序中的 [尋找所有參考] 工作。 按一下上方窗格中的任何項目，並在下方窗格中檢視指令碼內的實際變更 (以綠色反白顯示)。  
  
5.  按一下 **[套用]**。  
  
6.  請注意，針對已在資料表設計工具或 Transact\-SQL 編輯器中開啟的指令碼檔案，Transact\-SQL 編輯器已經以左邊綠色列反白顯示發生變更的位置。  
  
7.  請注意，[方案總管] 中加入的 [TradeDev.refactorlog]。 按兩下將它開啟。 它包含這個工作階段中所有變更的 XML 表示。  
  
8.  按 F5 建置並部署專案至本機資料庫。  
  
9. 以滑鼠右鍵按一下 [SQL Server 物件總管] 中 [本機] 下的 [TradeDev] 資料庫，然後選取 [重新整理]。  
  
10. 展開 [資料表]，並注意 [Products] 資料表已經重新命名。  
  
11. 以滑鼠右鍵按一下 [Product]，再選取 [檢視資料]。 請注意，無論是否有進行重新命名作業，現有的資料都保持完整無損。  
  
### <a name="to-expand-wildcards"></a>若要展開萬用字元  
  
1.  展開 [方案總管] 中的 [函式] 節點，然後按兩下 [GetProductsBySupplier.sql]。  
  
2.  將游標放在這一行的星號上，然後按一下滑鼠右鍵。 選取 [重構] 和 [展開萬用字元]。  
  
    ```  
    SELECT * from Product p  
    ```  
  
3.  在 [預覽變更] 對話方塊中，按一下上方窗格中的 `SELECT * from Product p` 加以反白顯示。  
  
4.  請注意，在下方的 [預覽變更] 窗格中，`*` 已經展開成下列內容。  
  
    ```  
    [Id], [Name], [ShelfLife], [SupplierId], [CustomerId]  
    ```  
  
5.  按一下 [套用] 按鈕。  請注意，這個編輯器再次以左邊綠色列反白顯示包含展開作業產生之變更的程式行。  
  
### <a name="to-fully-qualify-database-object-names"></a>若要完整限定資料庫物件名稱  
  
1.  確定 [GetProductsBySupplier.sql] 仍然在 Transact\-SQL 編輯器中開啟。  
  
2.  將游標放在這一行的 `Product` 上，然後按一下滑鼠右鍵。 選取 [重構] 和 [完整限定名稱]。  
  
    ```  
    SELECT [Id], [Name], [ShelfLife], [SupplierId], [CustomerId] from Product p  
    ```  
  
3.  按一下 [預覽變更] 對話方塊中的 [套用] 按鈕。  請注意，所有物件參考已經更新為包含物件的結構描述名稱，但是如果物件有父物件，則為父物件的名稱。  
  
    ```  
    SELECT [p].[Id], [p].[Name], [p].[ShelfLife], [p].[SupplierId], [p].[CustomerId] from [dbo].[Product] p  
    ```  
  
### <a name="to-move-schema"></a>若要移動結構描述  
  
1.  以滑鼠右鍵按一下您想要移動的物件。 選取 [重構] 和 [移動結構描述]。  
  
2.  在 [新結構描述] 清單中，按一下您想要將物件移入其中的結構描述名稱。 按一下 [確定]。  
  
    如果您選取了 [預覽變更] 核取方塊，就會顯示 [預覽變更] 對話方塊。 否則，系統會更新物件名稱，而且物件會移至新的結構描述。  
  
