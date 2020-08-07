---
title: 將存取應用程式連結至 SQL Server Azure SQL Database |Microsoft Docs
description: 瞭解如何將您的 Access 資料表連結到遷移的資料表，讓您可以使用現有的 Access 應用程式搭配 SQL Server 或 Azure SQL Database。
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
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
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: aadb041b3b9005d0e593e97974090250129ed33d
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823843"
---
# <a name="linking-access-applications-to-sql-server---azure-sql-database-accesstosql"></a>將存取應用程式連結至 SQL Server Azure SQL Database (AccessToSQL) 
如果您想要搭配使用現有的 Access 應用程式與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，可以將原始的 access 資料表連結到遷移 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 資料表。 連結會修改您的 Access 資料庫，讓您的查詢、表單、報表和資料存取頁面使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 資料庫中的資料，而非 Access 資料庫中的資料。  
  
> [!NOTE]  
> 您的存取資料表仍可繼續存取，但不會隨 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 更新一起更新。 連結資料表並確認功能之後，您可能會想要刪除存取資料表。  
  
## <a name="linking-access-and-sql-server-tables"></a>連結存取和 SQL Server 資料表  
當您將 Access 資料表連結到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Sql azure 資料表時，Jet 資料庫引擎會儲存連接資訊和資料表中繼資料，但資料會儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 sql azure 中。 雖然實際的資料表和資料位於或 SQL Azure 中，但此連結可讓您的存取應用程式對存取資料表進行操作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
> [!NOTE]  
> 如果您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，您的密碼會以純文字的方式儲存在連結的存取資料表上。 我們建議使用 Windows 驗證。  
  
**若要連結資料表**  
  
1.  在 [存取中繼資料 Explorer] 中，選取您想要連結的資料表。  
  
2.  以滑鼠右鍵按一下 [**資料表]**，然後選取 [**連結**]。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移轉小幫手 (SSMA) Access 會備份原始存取資料表並建立連結資料表。  
  
連結資料表之後，SSMA 中的資料表會顯示一個小的連結圖示。 在 [存取] 中，資料表會顯示「已連結」圖示，這是一個有箭號的地球。  
  
當您在 Access 中開啟資料表時，會使用索引鍵集資料指標來抓取資料。 因此，對於大型資料表，所有資料都不會一次抓取。 不過，當您流覽資料表時，Access 會視需要抓取其他資料。  
  
> [!IMPORTANT]  
> 若要連結 Azure 資料庫的存取資料表，您需要 SQL Server Native Client (SNAC) 10.5 版或更新版本。   
> 您可以從[Microsoft® SQL Server® 2008 R2 Feature Pack](https://www.microsoft.com/download/details.aspx?id=44272)取得最新版本的 SNAC。  
  
## <a name="unlinking-access-tables"></a>取消連結 Access 資料表  
當您從或 SQL Azure 資料表取消存取資料表的連結時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，SSMA 會還原原始的 access 資料表和其資料。  
  
**若要取消連結資料表**  
  
1.  在 [存取中繼資料 Explorer] 中，選取您要取消連結的資料表。  
  
2.  以滑鼠右鍵按一下 [**資料表]**，然後選取 [**取消連結**]。  
  
## <a name="linking-tables-to-a-different-server"></a>將資料表連結至不同的伺服器  
如果您已將 Access 資料表連結至一個 SQL Server 實例，而您稍後想要變更另一個實例的連結，則必須重新連結資料表。  
  
**若要將資料表連結至不同的伺服器**  
  
1.  在 [存取中繼資料 Explorer] 中，選取您要取消連結的資料表。  
  
2.  以滑鼠右鍵按一下 [**資料表]** ，然後選取 [**取消連結**]。  
  
3.  按一下 [**重新連線以 SQL Server** ] 按鈕。  
  
4.  連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 您要連結存取資料表的實例或 SQL Azure。  
  
5.  在 [存取中繼資料 Explorer] 中，選取您想要連結的資料表。  
  
6.  以滑鼠右鍵按一下 [**資料表]**，然後選取 [**連結**]。  
  
## <a name="updating-linked-tables"></a>更新連結資料表  
如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 變更或 SQL Azure 資料表定義，您可以使用本主題前面所示的程式，取消連結 SSMA 中的資料表，然後再將其重新連結。 您也可以使用 [存取] 來更新資料表。  
  
**若要使用存取權更新連結資料表**  
  
1.  開啟 Access 資料庫。  
  
2.  在 [**物件**] 清單中，按一下 [**資料表]**。  
  
3.  以滑鼠右鍵按一下連結資料表，然後選取 [**連結資料表管理員**]。  
  
4.  選取您要更新之每個連結資料表旁的核取方塊，然後按一下 **[確定]**。  
  
## <a name="possible-post-migration-issues"></a>可能的後續遷移問題  
下列各節列出在您將資料庫從存取權遷移至或 SQL Azure 之後，現有存取應用程式中可能發生的問題， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 然後連結資料表以及原因和解決方式。  
  
### <a name="slow-performance-with-linked-tables"></a>連結資料表的效能變慢  
**原因：** 基於下列原因，某些查詢可能會在轉換後緩慢：  
  
-   應用程式相依于不存在於或 SQL Azure 中的函式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，這會導致 Jet 在本機提取資料表以執行 SELECT 查詢。  
  
-   Jet 會傳送更新或刪除許多資料列的查詢，做為每個資料列的參數化查詢。  
  
**解決方式：** 將執行緩慢的查詢轉換成傳遞查詢、預存程式或 views。 轉換成傳遞查詢有下列問題：  
  
-   無法修改傳遞查詢。 修改查詢結果或加入新記錄必須以替代方式完成，例如，在表單上擁有明確的 [**修改**] 或 **[新增] 按鈕，** 並系結至查詢。  
  
-   有些查詢需要使用者輸入，但傳遞查詢不支援使用者輸入。 使用者輸入可以藉由 Visual Basic for Applications (VBA) 程式碼來取得，以提示輸入參數，或使用當做輸入控制項的表單。 在這兩種情況下，VBA 程式碼都會以使用者的輸入將查詢提交至伺服器。  
  
### <a name="auto-increment-columns-are-not-updated-until-the-record-is-updated"></a>自動遞增資料行在記錄更新之前不會更新  
**原因：** 通話記錄集之後，在 Jet 中進行 AddNew，在更新記錄之前，可以使用 [自動遞增] 資料行。 在或 SQL Azure 中，這不是 true [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 只有在儲存新記錄之後，才可以使用 [識別資料行] 新值的新值。  
  
**解決方式：** 在存取識別欄位之前，請先執行下列 Visual Basic for Applications (VBA) 程式碼：  
  
```  
Recordset.Update  
Recordset.Move 0,  
Recordset.LastModified  
```  
  
### <a name="new-records-are-not-available"></a>無法使用新的記錄  
**原因：** 當您使用 VBA 將記錄加入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 資料表時，如果資料表的唯一索引欄位具有預設值，而且您沒有指派值給該欄位，則在您重新開啟或 SQL Azure 中的資料表之前，新的記錄不會出現 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果您嘗試從新的記錄取得值，您會收到下列錯誤訊息：  
  
`Run-time error '3167' Record is deleted.`  
  
**解決方式：** 當您 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 VBA 程式碼開啟或 SQL Azure 資料表時，請包含 `dbSeeChanges` 選項，如下列範例所示：  
  
`Set rs = db.OpenRecordset("TestTable", dbOpenDynaset, dbSeeChanges)`  
  
### <a name="after-migration-some-queries-will-not-allow-the-user-to-add-a-new-record"></a>在遷移之後，某些查詢不會允許使用者新增記錄  
**原因：** 如果查詢不包含包含在唯一索引中的所有資料行，您就無法使用查詢來加入新的值。  
  
**解決方式：** 請確定至少包含一個唯一索引的所有資料行都是查詢的一部分。  
  
### <a name="you-cannot-modify-a-linked-table-schema-with-access"></a>您無法使用存取權修改連結資料表架構  
**原因：** 在遷移資料和連結資料表之後，使用者無法在存取中修改資料表的架構。  
  
**解決方式：** 使用修改資料表架構 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，然後更新 [存取] 中的連結。  
  
### <a name="hyperlink-functionality-is-lost-after-migrating-data"></a>在遷移資料之後遺失超連結功能  
**原因：** 在遷移資料之後，資料行中的超連結會失去其功能，並成為簡單的**Nvarchar (最大) **資料行。  
  
**解決方式︰** 無。  
  
### <a name="some-sql-server-data-types-are-not-supported-by-access"></a>存取不支援某些 SQL Server 資料類型  
**原因：** 如果您稍後將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 資料表更新為包含存取不支援的資料類型，就無法在存取中開啟資料表。  
  
**解決方式：** 您可以定義存取查詢，只傳回具有支援之資料類型的資料列。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
