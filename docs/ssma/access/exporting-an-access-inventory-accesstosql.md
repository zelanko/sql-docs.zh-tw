---
description: '匯出存取清查 (AccessToSQL) '
title: 匯出存取清查 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, exporting metadata
- exporting
- exporting Access metadata
- exporting, Access metadata
- exporting, querying exported metadata
- inventories of Access databases
- querying exported metadata
ms.assetid: 7e1941fb-3d14-4265-aff6-c77a4026d0ed
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 112452e9e6c31810dbf26d9aa1e7b36959c192d5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488331"
---
# <a name="exporting-an-access-inventory-accesstosql"></a>匯出存取清查 (AccessToSQL) 
如果您有多個 Access 資料庫，但不確定要遷移至哪一個資料庫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您可以匯出專案中所有 Access 資料庫的清查。 然後，您可以檢查和查詢清查中繼資料，以判斷這些資料庫中要遷移的資料庫和物件。 這項清查可讓您快速找到問題的解答，如下所示：  
  
-   最大的資料庫有哪些？  
  
-   誰擁有大部分的資料庫？  
  
-   哪些資料庫包含相同的資料表？  
  
-   過去六個月內未修改哪些資料庫？  
  
-   哪些資料庫包含私用資訊？  
  
本主題結尾會提供用來回答這些問題的查詢範例。  
  
## <a name="exported-metadata"></a>匯出的中繼資料  
SSMA 會匯出 Access 資料庫、資料表、資料行、索引、外鍵、查詢、報表、表單、宏和模組的相關中繼資料。 每個專案類別的相關中繼資料會匯出到個別的資料表。 如需這些資料表的架構，請參閱 [存取清查架構](access-inventory-schemas-accesstosql.md)。  
  
## <a name="exporting-inventory-data"></a>匯出清查資料  
若要匯出存取清查，您必須先開啟或建立 SSMA 專案，然後新增您想要分析的 Access 資料庫。 將資料庫加入至 SSMA 專案之後，您可以將這些資料庫的相關中繼資料匯出到指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫和架構。 如有必要，SSMA 會建立資料表來儲存中繼資料。 SSMA 接著會將 Access 資料庫的相關中繼資料加入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
> [!NOTE]  
> Access 資料庫可以分割成多個檔案：包含資料表和前端資料庫的後端資料庫，其中包含查詢、表單、報表、宏、模組和快速鍵。 如果您想要將分割資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請將前端資料庫新增至 SSMA。  
  
下列指示說明如何建立專案、將資料庫加入至專案、連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，然後匯出清查資料。  
  
**若要建立專案**  
  
1.  開啟 SSMA 以進行存取。  
  
2.  在 [檔案]**** 功能表上，選取 [新增專案]****。  
  
    [新增專案]  對話方塊隨即出現。  
  
3.  在 [ **名稱** ] 方塊中，輸入專案的名稱。  
  
4.  在 [ **位置** ] 方塊中，輸入或選取專案的資料夾。  
  
5.  在 [ **遷移至** ] 下拉式方塊中，選取您要遷移的目標版本，然後按一下 **[確定]**。  
  
如需建立專案的詳細資訊，請參閱 [建立和管理專案](creating-and-managing-projects-accesstosql.md)。  
  
**尋找和新增資料庫**  
  
1.  **在 [檔案**] 功能表上，按一下 [**尋找資料庫**]。  
  
2.  在 [尋找資料庫] 嚮導中，輸入您要搜尋的磁片磁碟機、檔案路徑或 UNC 路徑。 或者，按一下 **[流覽]** 以選取磁片磁碟機或網路資料夾。  
  
3.  按一下 [ **新增** ]，將位置加入清單方塊中。  
  
    重複上述兩個步驟，以新增其他搜尋位置。  
  
4.  （選擇性）加入搜尋條件，以精簡傳回的資料庫清單。  
  
    > [!IMPORTANT]  
    > [ **全部或部分的檔案名** ] 文字方塊不支援萬用字元。  
  
5.  按一下 [ **掃描**]。  
  
    [掃描] 頁面隨即出現。 這會顯示找到的資料庫和搜尋進度。 若要停止搜尋，請按一下 [ **停止**]。  
  
6.  在 [選取檔案] 頁面上，選取您要加入專案中的每個資料庫。  
  
    您可以使用清單頂端的 [全 **選** ] 和 [ **全部清除** ] 按鈕，以選取或清除所有資料庫。 您也可以按住 CTRL 鍵以選取多個資料列，或按住 SHIFT 鍵以選取某個範圍的資料列。  
  
7.  按一下 [下一步]  。  
  
8.  在 [驗證] 頁面上，按一下 **[完成]**。  
  
如需有關將資料庫加入至專案的詳細資訊，請參閱 [加入和移除 Access 資料庫](adding-and-removing-access-database-files-accesstosql.md)檔案。  
  
**若要連接到 SQL Server**  
  
1.  **在 [檔案**] 功能表上，選取 **[連接到 SQL Server]**。  
  
2.  在 [連接] 對話方塊中，輸入或選取實例的名稱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
    -   如果您要連接到本機電腦上的預設實例，可以輸入 **localhost** 或點 (**.**) 。  
  
    -   如果您要連接至另一部電腦上的預設實例，請輸入電腦的名稱。  
  
    -   如果您要連接到已命名的實例，請輸入電腦名稱稱、反斜線和實例名稱。 例如： MyServer\MyInstance。  
  
3.  在 [ **資料庫** ] 方塊中，輸入所匯出中繼資料的目標資料庫名稱。  
  
4.  如果您的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定為接受非預設通訊埠上的連接，請 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 [ **伺服器埠** ] 方塊中輸入用於連接的埠號碼。 若是的預設實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，預設的埠號碼為1433。 若為已命名的實例，SSMA 會嘗試從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 瀏覽器服務取得埠號碼。  
  
5.  在 [ **驗證** ] 下拉式功能表中，選取要用於連接的驗證類型。 若要使用目前的 Windows 帳戶，請選取 [ **Windows 驗證**]。 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，請選取 [ **SQL Server Authentication**]，然後提供使用者名稱和密碼。  
  
如需有關連接到的詳細資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請參閱 [連接到 SQL Server &#40;AccessToSQL&#41;](../../ssma/access/connecting-to-sql-server-accesstosql.md)。  
  
**匯出清查資訊**  
  
1.  在 Access 中繼資料瀏覽器中，展開 [ **存取-元**資料]。  
  
2.  選取 [ **資料庫**] 旁的核取方塊。  
  
    若要省略個別的資料庫或資料庫物件，請展開 [ **資料庫** ] 資料夾，然後清除資料庫或資料庫物件旁的核取方塊。  
  
3.  以滑鼠右鍵按一下 [ **資料庫** ]，然後選取 [ **匯出架構**]。  
  
4.  在 [ **選取匯出的架構** ] 對話方塊中，選取匯出中繼資料的目標架構，然後按一下 **[確定]**。  
  
每次您匯出中繼資料時，SSMA 會將資料附加至清查。 清查中的現有資料不會更新或刪除。  
  
## <a name="querying-the-exported-metadata"></a>查詢匯出的中繼資料  
匯出 Access 資料庫的相關中繼資料之後，您可以查詢中繼資料。 下列指示說明如何使用中的 [查詢編輯器] 視窗 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 執行查詢。  
  
**查詢中繼資料**  
  
1.  從 [ **開始** ] 功能表，依序指向 [ **所有程式**]、[ **microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005** ] 或 [microsoft ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008** ] 或 [ **microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012**]，然後按一下 [ **SQL Server Management Studio**]。  
  
2.  在 [ **連接到伺服器** ] 對話方塊中，確認設定，然後按一下 **[連接]**。  
  
3.  在 [Management Studio] 工具列上，按一下 [追加 **查詢** ] 開啟 [查詢編輯器]。  
  
4.  在 [查詢編輯器] 視窗中，輸入查詢。 下一節會顯示一些範例。  
  
5.  按 F5 鍵以執行查詢。  
  
## <a name="query-examples"></a>查詢範例  
在您執行下列任何查詢之前，您應該執行使用 *database_name* 查詢，以確定查詢是針對包含已匯出中繼資料的資料庫執行。 例如，如果您將中繼資料匯出至名為 MyAccessMetadata 的資料庫，您可以在程式碼的開頭新增下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 內容：  
  
```  
USE MyAccessMetadata;  
GO  
```  
下列範例全都使用 **dbo** 架構。 如果您將中繼資料匯出至另一個架構，請務必在執行這些查詢時變更架構。  
  
### <a name="what-tables-and-columns-are-in-these-databases"></a>這些資料庫中有哪些資料表和資料行？  
下列查詢會聯結包含資料行、資料表和資料庫中繼資料的資料表，然後傳回以資料行名稱排序的所有資料庫、資料表和資料行的名稱：  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D.DatabaseId  
ORDER BY ColumnName;  
```  
  
### <a name="what-are-the-largest-databases"></a>最大的資料庫有哪些？  
下列查詢會傳回資料庫名稱、檔案大小，以及每個 Access 資料庫中的資料表數目（依檔案大小排序）：  
  
```  
SELECT DatabaseName, FileSize, TablesCount  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileSize DESC;  
```  
  
### <a name="who-is-the-owner-of-most-of-the-databases"></a>誰是大部分資料庫的擁有者？  
下列查詢會傳回每個 Access 資料庫的資料庫名稱和擁有者，並依擁有者排序。  
  
```  
SELECT DatabaseName, FileOwner  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileOwner;  
```  
  
### <a name="which-databases-contain-the-same-tables"></a>哪些資料庫包含相同的資料表？  
下列查詢會使用子查詢來尋找在資料表清單中出現一次以上的所有資料表名稱，然後使用此資料表清單來取得資料庫名稱。 結果會傳回做為資料庫名稱，然後是資料表名稱，並依資料表名稱排序。  
  
```  
SELECT DatabaseName, TableName   
FROM dbo.SSMA_Access_InventoryTables T  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON D.DatabaseId = T.DatabaseId  
WHERE TableName IN (  
SELECT TableName   
FROM dbo.SSMA_Access_InventoryTables  
GROUP BY TableName   
HAVING count(*)>1  
)  
ORDER BY TableName;  
```  
  
### <a name="which-databases-were-not-modified-in-the-last-six-months"></a>過去六個月內未修改哪些資料庫？  
下列查詢會取得目前的日期，取得六個月前的月份值，然後傳回修改日期超過六個月前的資料庫清單。  
  
```  
SELECT DatabaseName, DateModified  
FROM dbo.SSMA_Access_InventoryDatabases  
WHERE DATEDIFF(month, DateModified, GETDATE()) > 6  
ORDER BY DateModified;  
```  
  
### <a name="which-databases-contain-private-information"></a>哪些資料庫包含私用資訊？  
您的 Access 資料庫可能包含機密資訊或個人資訊。 您可能會想要將這些資料庫移至，以利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 其安全性功能。 如果您知道包含機密資料的資料行有特定的名稱，或包含特定字元，您可以使用查詢來尋找包含該資訊的所有資料行。 例如，您可以尋找包含字串 "薪資" 的所有資料行。  然後查詢會傳回資料庫名稱、資料表名稱和資料行名稱。  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D. DatabaseId  
WHERE ColumnName LIKE '%salary%';  
```  
如果您不知道資料行名稱，您可以撰寫查詢來傳回所有資料行。 若要這樣做，請從上一個查詢中移除 WHERE 子句。  
  
## <a name="see-also"></a>另請參閱  
[準備 Access 資料庫以進行遷移](preparing-access-databases-for-migration-accesstosql.md)  
  
