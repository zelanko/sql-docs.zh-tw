---
title: 連結至 SQL Server-Azure SQL DB 存取應用程式 |Microsoft 文件
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access databases, linking to SQL Azure
- Access databases, linking to SQL Server
- auto-increment columns
- data types, unsupported
- hyperlink columns
- linking tables
- migrating databases, post-migration issues
- post-migration issues
- reference, post-migration issues
- refreshing linked tables
- slow performance
- unlinking tables
ms.assetid: 82374ad2-7737-4164-a489-13261ba393d4
caps.latest.revision: 19
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: e64bd412bc26dd2ac3cae24211591caa11f12031
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34774064"
---
# <a name="linking-access-applications-to-sql-server---azure-sql-db-accesstosql"></a>連結到 SQL Server-Azure SQL DB (AccessToSQL) 存取應用程式
如果您想要使用您現有的 Access 應用程式搭配[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您可以將原始的 Access 資料表連結至移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的資料表。 連結，讓您查詢、 表單、 報表和資料存取頁面使用中的資料會修改您的 Access 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫，而非 Access 資料庫中的資料。  
  
> [!NOTE]  
> 存取資料表保留在存取，但不是會更新並搭配[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 會更新。 在連結資料表，並驗證功能之後，您可能要刪除存取資料表。  
  
## <a name="linking-access-and-sql-server-tables"></a>連結的存取和 SQL Server 資料表  
當您連結來存取資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Jet 資料庫引擎 SQL Azure 資料表儲存連接資訊和資料表的中繼資料，但資料會儲存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 此連結可讓您存取應用程式對存取資料表即使實際的資料表和資料位於[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
> [!NOTE]  
> 如果您使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]連結存取資料表上的純文字儲存驗證，您的密碼。 我們建議使用 Windows 驗證。  
  
**若要連結資料表**  
  
1.  在存取中繼資料總管，選取您想要連結的資料表。  
  
2.  以滑鼠右鍵按一下**資料表**，然後選取**連結**。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 移轉小幫手 (SSMA) 的存取會備份原始的 Access 資料表，並建立連結的資料表。  
  
連結資料表之後，SSMA 這些資料表會顯示一個小型的連結圖示。 在 Access 中，這些資料表會顯示 「 連結 」 的圖示，即箭號指向它的地球。  
  
當您在 Access 中開啟資料表時，使用索引鍵集資料指標擷取的資料。 因此，對於大型資料表，所有的資料不會擷取一次。 不過，當您瀏覽資料表時，存取擷取需要的其他資料。  
  
> [!IMPORTANT]  
> 若要與 Azure 的資料庫的 access 資料表連結，您需要 SQL Server 原生 Client(SNAC) 10.5 或更新版本。   
> 您可以取得最新版的 SNAC 從[Microsoft® SQL Server® 2008 R2 功能套件](http://go.microsoft.com/fwlink/?LinkId=196940)。  
  
## <a name="unlinking-access-tables"></a>正在取消連結存取資料表  
當您取消連結從 Access 資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料表，SSMA 還原原始的 Access 資料表及其資料。  
  
**若要取消連結資料表**  
  
1.  在存取中繼資料總管，選取您想要取消連結的資料表。  
  
2.  以滑鼠右鍵按一下**資料表**，然後選取**取消**。  
  
## <a name="linking-tables-to-a-different-server"></a>將資料表連結至另一部伺服器  
如果您的 Access 資料表連結至一個 SQL Server 執行個體，您稍後想要變更連結至另一個執行個體，您必須重新連結資料表。  
  
**若要連結至不同的伺服器資料表**  
  
1.  在存取中繼資料總管，選取您想要取消連結的資料表。  
  
2.  以滑鼠右鍵按一下**資料表**，然後選取 **取消**。  
  
3.  按一下**重新連接到 SQL Server**  按鈕。  
  
4.  連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或您要的 Access 資料表連結的 SQL Azure。  
  
5.  在存取中繼資料總管，選取您想要連結的資料表。  
  
6.  以滑鼠右鍵按一下**資料表**，然後選取**連結**。  
  
## <a name="updating-linked-tables"></a>更新連結的資料表  
如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料表定義會變更，您可以取消連結，然後使用先前在本主題中顯示的程序重新連結 SSMA 中的資料表。 您也可以使用存取更新的資料表。  
  
**若要使用存取更新連結的資料表**  
  
1.  開啟存取資料庫。  
  
2.  在**物件**清單中，按一下**資料表**。  
  
3.  連結的資料表，請以滑鼠右鍵按一下，然後選取**連結資料表管理員**。  
  
4.  選取您想要更新，然後按一下每個連結表旁邊的核取方塊**確定**。  
  
## <a name="possible-post-migration-issues"></a>可能的移轉後問題  
下面各節清單問題之後將資料庫從存取移轉現有的存取應用程式中可能發生[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，然後連結資料表，以及原因，並解決問題。  
  
### <a name="slow-performance-with-linked-tables"></a>連結的資料表的效能變慢  
**原因：** 有些查詢可能會變慢轉換之後，原因如下：  
  
-   應用程式相依於函式，不存在於[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，這會導致 Jet 以提取在本機執行 SELECT 查詢的資料表。  
  
-   更新或刪除多個資料列的查詢所傳送 Jet 做為參數化查詢的每個資料列。  
  
**解決方式：** 轉換傳遞查詢、 預存程序或檢視表的查詢執行緩慢。 轉換為傳遞查詢有下列問題：  
  
-   無法修改通過查詢。 修改查詢結果，或加入新的記錄必須由在另一種，例如具有明確**修改**或**新增**繫結至查詢在表單上的按鈕。  
  
-   某些查詢需要使用者輸入，但傳遞的查詢不支援使用者輸入。 Visual Basic for Applications (VBA) 程式碼會提示輸入參數，或做為輸入控制項的表單，可取得使用者輸入。 在這兩種情況下，VBA 程式碼會送出具有伺服器的使用者輸入的查詢。  
  
### <a name="auto-increment-columns-are-not-updated-until-the-record-is-updated"></a>自動遞增資料行更新才會更新的記錄  
**原因：** 之後呼叫 RecordSet.AddNew Jet 中時，自動遞增資料行便會更新的記錄之前。 這不是 true[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 只有在儲存新的記錄之後有識別資料行的新值的新值。  
  
**解決方式：** 存取識別欄位之前，先執行下列 Visual Basic for Applications (VBA) 程式碼：  
  
```  
Recordset.Update  
Recordset.Move 0,  
Recordset.LastModified  
```  
  
### <a name="new-records-are-not-available"></a>未提供新的記錄  
**原因：** 當您將記錄新增至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料表，則資料表的唯一索引欄位的預設值，而且您沒有指派值給該欄位中，新的記錄不會出現直到您重新開啟的資料表中使用 VBA[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 如果您嘗試從新的記錄取得值，您會收到下列錯誤訊息：  
  
`Run-time error '3167' Record is deleted.`  
  
**解決方式：** 當您開啟[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料表使用 VBA 程式碼中包含`dbSeeChanges`選項，如下列範例所示：  
  
`Set rs = db.OpenRecordset("TestTable", dbOpenDynaset, dbSeeChanges)`  
  
### <a name="after-migration-some-queries-will-not-allow-the-user-to-add-a-new-record"></a>移轉之後，有些查詢將不允許使用者新增新的記錄  
**原因：** 如果查詢未包含唯一索引中包含的所有資料行，您無法使用查詢來加入新的值。  
  
**解決方式：** 確保至少一個唯一索引中包含的所有資料行查詢的一部分。  
  
### <a name="you-cannot-modify-a-linked-table-schema-with-access"></a>您無法修改連結的資料表結構描述具有存取權  
**原因：** 後移轉資料和連結的資料表，使用者就無法修改資料表中存取的結構描述。  
  
**解決方式：** 修改資料表結構描述使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]，然後更新中存取的連結。  
  
### <a name="hyperlink-functionality-is-lost-after-migrating-data"></a>超連結功能，在移轉之後會遺失資料  
**原因：** 之後移轉資料，資料行中的超連結失去其功能，而變得簡單**nvarchar （max)** 資料行。  
  
**解決方式：** None。  
  
### <a name="some-sql-server-data-types-are-not-supported-by-access"></a>存取不支援某些 SQL Server 資料類型  
**原因：** 如果您之後要更新您[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料表来包含的資料類型，不會受到存取，您無法在 Access 中開啟資料表。  
  
**解決方式：** 您可以定義存取查詢傳回的資料列與支援的資料類型。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
