---
title: 連結至 SQL Server-Azure SQL DB 的存取應用程式 |Microsoft Docs
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
ms.openlocfilehash: 20efdf681baa8305b3b2be08b2e9f3efe999d3fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62760139"
---
# <a name="linking-access-applications-to-sql-server---azure-sql-db-accesstosql"></a>連結到 SQL Server-Azure SQL DB (AccessToSQL) 存取應用程式
如果您想要使用您現有的 Access 應用程式搭配[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以將原始的 Access 資料表連結至移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料表。 連結，讓您查詢、 表單、 報表和資料存取頁面使用中的資料會修改您的 Access 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料庫，而非 Access 資料庫中的資料。  
  
> [!NOTE]  
> 存取資料表保持在 Access 中，但不是會更新並搭配[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 的更新。 連結資料表後，當您驗證功能，您可能想要刪除存取資料表。  
  
## <a name="linking-access-and-sql-server-tables"></a>連結 Access 和 SQL Server 資料表  
若要存取資料表的連結時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料表，Jet database engine 會儲存連接資訊和資料表中繼資料，但資料會儲存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 此連結可讓您存取應用程式對存取資料表即使實際的資料表和資料位於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
> [!NOTE]  
> 如果您使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證，您的密碼會儲存在連結的 Access 資料表上的純文字。 我們建議使用 Windows 驗證。  
  
**若要連結資料表**  
  
1.  在存取中繼資料總管 中，選取您想要連結的資料表。  
  
2.  以滑鼠右鍵按一下**資料表**，然後選取**連結**。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移轉小幫手 (SSMA) 的存取會備份原始的 Access 資料表，並建立連結的資料表。  
  
連結資料表之後，在 SSMA 中的資料表會出現小型的連結圖示。 在 Access 中，資料表會出現 「 已連結 」 圖示，即箭號指向它的地球。  
  
當您在 Access 中開啟資料表時，使用索引鍵集資料指標擷取資料。 如此一來，針對大型資料表時，所有的資料不會擷取一次。 不過，當您瀏覽資料表時，存取會擷取為所需的其他資料。  
  
> [!IMPORTANT]  
> 若要使用的 Azure 資料庫的 access 資料表連結，您需要 SQL Server 原生 Client(SNAC) 版本 10.5 或更新版本。   
> 您可以取得最新版的從 SNAC [Microsoft® SQL Server® 2008 R2 功能套件](https://go.microsoft.com/fwlink/?LinkId=196940)。  
  
## <a name="unlinking-access-tables"></a>取消連結存取資料表  
當您取消連結從 Access 資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料表，SSMA 還原原始的 Access 資料表及其資料。  
  
**若要取消連結資料表**  
  
1.  在存取中繼資料總管 中，選取您想要取消連結的資料表。  
  
2.  以滑鼠右鍵按一下**資料表**，然後選取**取消連結**。  
  
## <a name="linking-tables-to-a-different-server"></a>將資料表連結至另一部伺服器  
如果 Access 資料表連結至 SQL Server 執行個體，您稍後想要變更連結至另一個執行個體，您必須重新連結的資料表。  
  
**若要連線到不同的伺服器的資料表**  
  
1.  在存取中繼資料總管 中，選取您想要取消連結的資料表。  
  
2.  以滑鼠右鍵按一下**資料表**，然後選取**取消連結**。  
  
3.  按一下 [**重新連接到 SQL Server** ] 按鈕。  
  
4.  連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或您要的 Access 資料表連結的 SQL Azure。  
  
5.  在存取中繼資料總管 中，選取您想要連結的資料表。  
  
6.  以滑鼠右鍵按一下**資料表**，然後選取**連結**。  
  
## <a name="updating-linked-tables"></a>更新連結的資料表  
如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料表定義會改變，您可以取消連結，然後再使用先前在本主題所示的程序重新連結 SSMA 中的資料表。 您也可以使用存取更新的資料表。  
  
**若要使用存取更新連結的資料表**  
  
1.  開啟 Access 資料庫。  
  
2.  在 **物件**清單中，按一下**資料表**。  
  
3.  以滑鼠右鍵按一下 連結的資料表，然後按**連結資料表管理員**。  
  
4.  選取您想要更新，並按一下每個連結資料表旁的核取方塊**確定**。  
  
## <a name="possible-post-migration-issues"></a>可能的移轉後問題  
下列各節的清單存取從移轉資料庫之後，現有的 Access 應用程式中可能發生的問題[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，然後連結資料表，以及原因和解決方式。  
  
### <a name="slow-performance-with-linked-tables"></a>連結的資料表的效能變慢  
**原因：** 有些查詢可能會變慢之後轉換原因如下：  
  
-   應用程式相依於函式，不存在於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，這會導致 Jet 能夠提取在本機執行 SELECT 查詢的資料表。  
  
-   更新或刪除多個資料列的查詢會傳送 Jet 做為參數化查詢每個資料列。  
  
**解決方案：** 轉換傳遞查詢、 預存程序或檢視表的查詢執行緩慢。 將轉換成傳遞查詢有下列問題：  
  
-   無法修改傳遞查詢。 修改查詢結果，或加入新的記錄中，必須完成的替代方式，例如藉由明確**修改**或是**新增**您繫結至查詢的表單上的按鈕。  
  
-   某些查詢需要使用者輸入，但傳遞的查詢不支援使用者輸入。 Visual Basic for Applications (VBA) 程式碼會提示您輸入參數，或做為輸入的控制項的表單，您可以取得使用者輸入。 在這兩種情況下，VBA 程式碼會提交至伺服器的使用者輸入的查詢。  
  
### <a name="auto-increment-columns-are-not-updated-until-the-record-is-updated"></a>更新記錄之前，不會更新自動遞增資料行  
**原因：** 之後呼叫 RecordSet.AddNew Jet 中，自動遞增資料行隨即出現，才會更新記錄。 這不是在 true[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 儲存新的記錄後，才可的身分識別資料行的新值的新值。  
  
**解決方案：** 執行下列 Visual Basic for Applications (VBA) 程式碼才能存取 [身分識別] 欄位：  
  
```  
Recordset.Update  
Recordset.Move 0,  
Recordset.LastModified  
```  
  
### <a name="new-records-are-not-available"></a>未提供新的記錄  
**原因：** 當您將記錄新增至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料表，如果資料表的唯一索引欄位的預設值，而您不指派值至該欄位中，不會出現新的記錄直到您重新開啟中的資料表使用 VBA，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 如果您嘗試取得新的記錄中的值，您會收到下列錯誤訊息：  
  
`Run-time error '3167' Record is deleted.`  
  
**解決方案：** 當您開啟[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料表使用 VBA 程式碼中包含`dbSeeChanges`選項，如下列範例所示：  
  
`Set rs = db.OpenRecordset("TestTable", dbOpenDynaset, dbSeeChanges)`  
  
### <a name="after-migration-some-queries-will-not-allow-the-user-to-add-a-new-record"></a>移轉之後，某些查詢將不允許使用者加入新的記錄  
**原因：** 如果查詢不包含唯一的索引中包含的所有資料行，您無法使用查詢來加入新的值。  
  
**解決方案：** 確定至少一個唯一的索引中包含的所有資料行查詢的一部分。  
  
### <a name="you-cannot-modify-a-linked-table-schema-with-access"></a>您無法修改連結的資料表結構描述具有存取權  
**原因：** 移轉資料和連結的資料表之後, 使用者就無法修改 Access 中的資料表結構的描述。  
  
**解決方案：** 修改資料表結構描述使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然後更新中存取的連結。  
  
### <a name="hyperlink-functionality-is-lost-after-migrating-data"></a>超連結功能在移轉之後會遺失資料  
**原因：** 移轉之後資料行中的超連結會失去其功能和變得簡單**nvarchar （max)** 資料行。  
  
**解決方案：** 無。  
  
### <a name="some-sql-server-data-types-are-not-supported-by-access"></a>存取不支援某些 SQL Server 資料類型  
**原因：** 如果您稍後可以更新您[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料表來包含資料類型不支援的存取權，您無法在 Access 中開啟資料表。  
  
**解決方案：** 您可以定義 Access 查詢會傳回只支援的資料類型與資料列。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
