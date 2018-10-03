---
title: 如何：建立專案的快照集 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.SqlProjectImportSnapshotSummaryDialog.dialog
- sql.data.tools.SqlProjectImportSnapshotDialog.dialog
ms.assetid: bed670a3-13bd-4d88-91a1-58d5b9524a97
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b7215ed9f2374a46ffd5034ce8a85ab0f40419ed
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840226"
---
# <a name="how-to-create-a-snapshot-of-a-project"></a>如何：建立專案的快照集
**資料層應用程式**檔案提供了資料庫結構描述建立當時的唯讀表示。 其本質上被視為資料庫結構描述，您可以從中將結構描述物件匯回專案。 您也可以將它與資料庫或專案的結構描述進行比較，然後更新資料庫或專案以反映快照集之中定義的結構描述。  
  
在來源資料庫專案發生使用者錯誤的情況下，您可以將該來源專案還原為它在快照集建立時所處於的狀態。 基於比較基準的目的，您也可以在各個開發階段建立快照集。  
  
> [!WARNING]  
> 下列程序利用先前在[連接的資料庫開發](../ssdt/connected-database-development.md)和[專案導向的離線資料庫開發](../ssdt/project-oriented-offline-database-development.md)小節中的程序所建立的實體。  
  
### <a name="to-create-a-snapshot"></a>若要建立快照集  
  
1.  以滑鼠右鍵按一下 [方案總管] 中的 [TradeDev] 專案，再選取 [資料層應用程式 (\*.dacpac)]。  
  
2.  SSDT 將先嘗試建置專案。 如果沒有發生建置錯誤，[Snapshot] 資料夾會建立在 [方案總管] 中。 在這個資料夾內，SSDT 會以「<Project Name>_YYYYMMDD_HH-MM-SS.dacpac」名稱格式建立 .dacpac 檔案。  
  
3.  以滑鼠右鍵按一下 .dacpac 檔案，再選取 [重新命名]。 將預設檔名變更為 "TradeDev1.dacpac"。  
  
4.  以滑鼠右鍵按一下 [方案總管] 中的 [GetProductsBySupplier] 函式，再選取 [刪除] 將它從專案中移除。  
  
5.  按照前面的步驟，建立一個叫做 **TradeDev2.dacpac** 的新快照集。  
  
### <a name="to-import-a-snapshot"></a>若要匯入快照集  
  
1.  以滑鼠右鍵按一下 [方案總管] 中的 [TradeDev] 專案，再從內容功能表中依序選取 [匯入]、[資料層應用程式 (\*.dacpac)] 。  
  
2.  在 [匯入資料層應用程式] 對話方塊中，按一下 [瀏覽] 選取 **TradeDev1.dacpac** 做為匯入的來源。  
  
    請注意，[目標專案] 區段已停用，因為目前專案是預設目標。 按一下 [開始] 開始進行匯入。  
  
3.  按一下 [摘要] 頁面中的 [完成]。 請注意，在 [方案總管] 中，被刪除的資料表已經還原至專案。  
  
    > [!WARNING]  
    > 匯入快照集會將快照集結構描述中的所有資料庫實體都匯入至專案， 因此可能會建立重複的實體。 例如，每個資料表和檢視表現在都包含本身的額外複本，它的名稱為 <ObjectName_1>。 在 [方案總管] 中，以滑鼠右鍵按一下每一個重複的物件，再選取 [刪除] 將它從專案中移除。  
  
### <a name="to-compare-snapshots"></a>若要比較快照集  
  
1.  以滑鼠右鍵按一下 [方案總管] 中的 [TradeDev1.dacpac]，再選取 [結構描述比較]。 [結構描述比較] 視窗隨即開啟。  
  
2.  使用 [資料層應用程式檔案] 選項設定來源與目標結構描述。 請確認在 [資料層應用程式檔案] 中，[來源結構描述] 設定為 [TradeDev1.dacpac]，[目標結構描述] 設定為 [TradeDev2.dacpac]。  
  
3.  按一下 [確定] 開始進行比較。 請注意，被刪除的函式在新舊快照集之間會以反白顯示為差異。  
  
    使用 [結構描述比較]，您可以輕鬆地尋找不同快照集的差異。 在這種情況下，您可以找出專案在開發過程中的成長方式。  
  
## <a name="see-also"></a>另請參閱  
[如何：使用結構描述比較，比較不同的資料庫定義](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)  
  
