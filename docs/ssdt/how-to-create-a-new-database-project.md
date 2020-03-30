---
title: 建立新的資料庫專案
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.dbprojectwizard.importschema
- sql.data.tools.SqlProjectImportDatabaseDialog.dialog
- sql.data.tools.importscriptwizard.welcome
- sql.data.tools.importscriptwizard.summary
- sql.data.tools.SqlProjectImportDatabaseSummaryDialog.dialog
- sql.data.tools.importscriptwizard.fileselection
ms.assetid: 0b7883fa-b6e1-4ccf-b1d8-f522fd03a59d
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 3ce0ac6afc902803afe8aa6e20c71f38998f8286
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75241541"
---
# <a name="how-to-create-a-new-database-project"></a>如何：建立新的資料庫專案

您可以建立新的資料庫專案，並從現有的資料庫、.sql 指令碼檔案或資料層應用程式 (.dacpac) 匯入資料庫結構描述。 接著，您可以叫用相同的視覺化設計工具 (Transact\-SQL 編輯器、資料表設計工具)，讓連接的資料庫開發工作變更離線資料庫專案，並將變更發行回生產資料庫。 變更也可以另存成指令碼，等以後再發行。 使用 [專案屬性]  窗格，您可以將目標平台變更為其他版本的 SQL Server (包括 SQL Azure)。  
  
下列兩個程序建立新的資料庫專案並從現有的資料庫匯入結構描述，在本質上達到相同的目標。 每個資料庫物件在 [方案總管]  中都將呈現為 SQL 指令碼檔案 (.sql)。 如需有關從快照集匯入資料庫結構描述的詳細資訊，請參閱[如何：建立專案的快照集](../ssdt/how-to-create-a-snapshot-of-a-project.md)。  
  
> [!WARNING]  
> 下列程序將利用先前在[連接的資料庫開發](../ssdt/connected-database-development.md)小節的程序中所建立的實體。  
  
### <a name="to-create-a-new-database-project-off-a-connected-database"></a>若要從連接的資料庫建立新的資料庫專案  
  
1.  以滑鼠右鍵按一下 [SQL Server 物件總管]  中的 [TradeDev]  節點，再選取 [建立新專案]  。  
  
2.  在 [匯入資料庫]  對話方塊中，請注意 [來源資料庫連接]  設定已由您在 [SQL Server 物件總管]  中選取的資料庫預先定義。 在 [目標專案]  設定中，將專案名稱變更為 **TradeDev**。  
  
3.  在 [匯入設定]  區段中，請注意那些用於匯入特定物件與設定以及用於為每個結構描述和/或物件類型建立資料夾的選項。 針對所有資料庫物件的組織化階層接受預設值，然後按一下 [開始]  。  
  
4.  [匯入資料庫]  對話方塊隨即顯示一個進度列和正在匯入的 SSDT 物件清單。 在匯入作業完成後，按一下 [完成]  結束最後的畫面。  
  
5.  檢查 [方案總管]  中的階層。 展開 [dbo]  資料夾，您會發現個別的 [函式]  、[資料表]  和 [檢視表]  資料夾。 請注意，資料表和函式在其結構描述資料夾下是分組排列的。  
  
6.  按兩下 [資料表]  底下的 [Products.sql]  。 [資料表設計工具]  隨即開啟，在資料行格線中顯示資料表的視覺化解譯，並在指令碼窗格顯示資料表的指令碼定義。 這等同於在我們看到的內容[連接的資料庫開發](../ssdt/connected-database-development.md)一節。  
  
7.  取消選取 [CustomerId]  資料行的 [允許 Null]  方塊。 按 CTRL + S 儲存檔案。  
  
8.  以滑鼠右鍵按一下 [方案總管]  中的 [TradeDev]  專案，再選取 [建置]  建置該資料庫專案。  
  
    您可以在 [輸出] 視窗中看到建置作業的結果。  
  
### <a name="to-create-a-new-project-and-import-existing-database-schema"></a>若要建立新的專案並匯入現有的資料庫結構描述  
  
1.  依序按一下 [檔案]  、[新增]  和 [專案]  。 在 [新增專案]  對話方塊中，選取左窗格中的 [SQL Server]  。 請注意，只有一個資料庫專案類型：[SQL Server 資料庫專案]  。 和舊版 Visual Studio 一樣，沒有平台特定的專案。 在專案建立後，您便可以在 [專案設定]  對話方塊中設定目標平台。 這類工作會涵蓋在[如何：變更目標平台及發行資料庫專案](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)主題中。  
  
2.  將專案名稱變更為 **TradeDev**，然後按一下 [確定]  建立新專案。  
  
3.  在 [方案總管]  中，以滑鼠右鍵按一下新建的 **TradeDev** 專案，再依序選取 [匯入]  和 [資料庫]  。  
  
    [匯入資料庫]  對話方塊隨即開啟。 按一下 [來源資料庫連接]  區段中的 [選擇資料庫]  ，然後選取 [TradeDev]  。 如果 [TradeDev]  不在下拉式清單中，請使用 [新增連接]  按鈕編輯 [連接屬性]。  
  
4.  在 [匯入設定]  區段中，請注意那些用於匯入特定物件與設定以及用於為每個結構描述和/或物件類型建立資料夾的選項。 針對所有資料庫物件的組織化階層接受預設值，然後按一下 [開始]  。  
  
5.  [匯入資料庫]  對話方塊隨即顯示一個進度列和正在匯入的 SSDT 物件清單。 在匯入作業完成後，按一下 [完成]  結束最後的畫面。  
  
6.  檢查 [方案總管]  中的階層。 展開 [dbo]  資料夾，您會發現個別的 [函式]  、[資料表]  和 [檢視表]  資料夾。 請注意，資料表和函式在其結構描述資料夾下是分組排列的。  
  
7.  按兩下 [資料表]  底下的 [Products.sql]  。 [資料表設計工具]  隨即開啟，在資料行格線中顯示資料表的視覺化解譯，並在指令碼窗格顯示資料表的指令碼定義。 這等同於在我們看到的內容[連接的資料庫開發](../ssdt/connected-database-development.md)一節。  
  
8.  取消選取 [CustomerId]  資料行的 [允許 Null]  方塊。 按 CTRL + S 儲存檔案。  
  
9. 以滑鼠右鍵按一下 [方案總管]  中的 [TradeDev]  專案，再選取 [建置]  建置該資料庫專案。  
  
## <a name="see-also"></a>另請參閱  
[如何：變更目標平台及發行資料庫專案](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)  
  
