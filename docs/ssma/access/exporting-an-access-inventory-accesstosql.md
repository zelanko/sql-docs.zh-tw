---
title: "匯出存取清查 (AccessToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 55f91e6b5e83b3a317f74b71e591de7e08009413
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="exporting-an-access-inventory-accesstosql"></a>匯出存取清查 (AccessToSQL)
如果您有多個存取資料庫，而且您不確定要將移轉至哪些[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您可以匯出專案中的所有存取資料庫的清查。 您可以檢閱，然後查詢來判斷哪一個資料庫並移轉這些資料庫中的物件的清查中繼資料。 這個清查可讓您快速尋找問題解答，如下所示：  
  
-   最大的資料庫有哪些？  
  
-   大部分的資料庫擁有者是誰？  
  
-   資料庫包含相同的資料表？  
  
-   過去六個月內尚未經過修改的資料庫？  
  
-   資料庫包含個人資訊？  
  
本主題結尾處提供用來回答下列問題的查詢範例。  
  
## <a name="exported-metadata"></a>匯出的中繼資料  
SSMA 會將匯出有關存取資料庫、 資料表、 資料行、 索引、 外部索引鍵、 查詢、 報告、 表單、 巨集和模組的中繼資料。 每個項目分類的相關中繼資料匯出至不同的資料表。 這些資料表的結構描述，請參閱[存取清查結構描述](http://msdn.microsoft.com/en-us/fdd3cff2-4d62-4395-8acf-71ea8f17f524)。  
  
## <a name="exporting-inventory-data"></a>匯出清查資料  
若要匯出的存取詳細目錄，您必須第一次開啟或建立 SSMA 專案，然後再新增 [您想要分析的 Access 資料庫。 SSMA 專案中加入資料庫之後，您匯出這些資料庫的相關中繼資料指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫和結構描述。 如有必要，SSMA 會建立資料表來儲存的中繼資料。 SSMA，然後將 Access 資料庫的相關中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。  
  
> [!NOTE]  
> Access 資料庫可以分成多個檔案： 包含資料表和包含查詢、 表單、 報表、 巨集、 模組和快速鍵的前端資料庫後端資料庫。 如果您想要分割資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，加入 SSMA 的前端資料庫。  
  
下面的指示說明如何建立專案、 將資料庫加入至專案、 連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，，然後匯出清查資料。  
  
**若要建立專案**  
  
1.  開啟 SSMA 進行存取。  
  
2.  在 [檔案] 功能表上，選取 [新增專案]。  
  
    [新增專案]  對話方塊隨即出現。  
  
3.  在**名稱**方塊中，輸入您的專案名稱。  
  
4.  在**位置**方塊中，輸入或選取專案的資料夾。  
  
5.  在**移轉至**下拉式方塊中，選取您想要移轉，然後按一下的目標版本**確定**。  
  
如需有關如何建立專案的詳細資訊，請參閱[建立和管理專案](http://msdn.microsoft.com/en-us/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7)。  
  
**若要找出並新增資料庫**  
  
1.  在**檔案**功能表上，按一下 [**尋找資料庫**。  
  
2.  在 [尋找資料庫精靈] 中，輸入磁碟機、 檔案路徑或您想要搜尋的 UNC 路徑。 或者，按一下**瀏覽**以選取的磁碟機或網路資料夾。  
  
3.  按一下**新增**加入清單方塊的位置。  
  
    重複上述步驟來新增其他搜尋位置。  
  
4.  或者，新增搜尋準則來調整資料庫所傳回的清單。  
  
    > [!IMPORTANT]  
    > **全部或部份檔案名稱**文字方塊中不支援萬用字元。  
  
5.  按一下**掃描**。  
  
    掃描頁面隨即出現。 這會顯示發現的資料庫，並搜尋進度。 若要停止搜尋，請按一下**停止**。  
  
6.  在 [選取檔案] 頁面中，選取您想要加入至專案的每個資料庫。  
  
    您可以使用**全選**和**全部清除**加以選取或清除所有的資料庫清單頂端的按鈕。 您也可以按住 CTRL 鍵以選取多個資料列，或按住 SHIFT 鍵向選取的資料列範圍。  
  
7.  按一下 **[下一步]**。  
  
8.  在確認頁面上，按一下 [**完成**。  
  
如需有關如何將資料庫加入至專案的詳細資訊，請參閱[加入和移除的 Access 資料庫檔案](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)。  
  
**若要連接到 SQL Server**  
  
1.  在**檔案**功能表上，選取**連接到 SQL Server**。  
  
2.  在 [連線] 對話方塊中，輸入或選取的執行個體名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
    -   如果您要連接到本機電腦上的預設執行個體，您可以輸入**localhost**或一個點 (**。**)。  
  
    -   如果您要連接到另一部電腦上的預設執行個體，請輸入電腦的名稱。  
  
    -   如果您要連接到具名執行個體，請輸入電腦名稱、 反斜線和執行個體名稱。 例如： MyServer\MyInstance。  
  
3.  在**資料庫**方塊中，輸入匯出的中繼資料的目標資料庫的名稱。  
  
4.  如果您的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]設定為非預設連接埠上接受連接，請輸入用於連接埠號碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中的連線**伺服器連接埠**方塊。 預設執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，預設連接埠號碼為 1433年。 具名執行個體，SSMA 會嘗試取得連接埠號碼從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]瀏覽器服務。  
  
5.  在**驗證**下拉式功能表，選取要用於連線的驗證類型。 若要使用目前的 Windows 帳戶，請選取**Windows 驗證**。 若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登入，選取**SQL Server 驗證**，然後提供使用者名稱和密碼。  
  
如需有關連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，請參閱[連接到 SQL Server & #40;AccessToSQL & #41;](../../ssma/access/connecting-to-sql-server-accesstosql.md).  
  
**若要匯出清查資訊**  
  
1.  在存取中繼資料總管]，依序展開**存取 metabase**。  
  
2.  選取此核取方塊旁的 [**資料庫**。  
  
    若要省略個別的資料庫或資料庫物件，請展開**資料庫**資料夾，然後再清除資料庫或資料庫物件旁邊的核取方塊。  
  
3.  以滑鼠右鍵按一下**資料庫**選取**匯出結構描述**。  
  
4.  在**選取匯出的結構描述**對話方塊中，選取匯出的中繼資料的目標結構描述，然後按一下**確定**。  
  
匯出中繼資料，每次 SSMA 會將資料附加到清查。 無法更新或刪除在清查中現有的資料。  
  
## <a name="querying-the-exported-metadata"></a>查詢所匯出中繼資料  
匯出有關存取資料庫的中繼資料之後，您可以查詢中繼資料。 若要使用查詢編輯器] 視窗中的下列指示描述[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]來執行查詢。  
  
**若要查詢的中繼資料**  
  
1.  從**啟動**功能表上，指向**所有程式**，指向 [ **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005年**或**Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008年**或**Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012年**，然後按一下 [ **SQL Server Management Studio**。  
  
2.  在**連接到伺服器**對話方塊中，確認設定，然後按一下**連接**。  
  
3.  Management Studio 工具列上，按一下**新查詢**開啟查詢編輯器。  
  
4.  在 [查詢編輯器] 視窗中，輸入查詢。 下一節顯示一些範例。  
  
5.  按 F5 鍵以執行查詢。  
  
## <a name="query-examples"></a>查詢範例  
執行下列查詢之前，您應該執行使用*database_name*先確定查詢會針對包含匯出的中繼資料的資料庫執行查詢。 例如，如果您的中繼資料匯出至名為 MyAccessMetadata 資料庫時，您會加入下列的開頭[!INCLUDE[tsql](../../includes/tsql_md.md)]程式碼：  
  
```  
USE MyAccessMetadata;  
GO  
```  
下列範例都會使用**dbo**結構描述。 如果您另一個結構描述匯出中繼資料，請務必變更結構描述，當您執行這些查詢。  
  
### <a name="what-tables-and-columns-are-in-these-databases"></a>有哪些資料表和資料行？ 這些資料庫中  
下列查詢聯結包含資料行、 資料表和資料庫中繼資料的資料表，然後傳回 [所有資料庫、 資料表和資料行，排序資料行名稱的名稱：  
  
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
下列查詢會傳回資料庫名稱、 檔案大小和數目的資料表中每個存取資料庫，依照檔案大小：  
  
```  
SELECT DatabaseName, FileSize, TablesCount  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileSize DESC;  
```  
  
### <a name="who-is-the-owner-of-most-of-the-databases"></a>大部分的資料庫擁有者是誰？  
下列查詢會傳回資料庫名稱和擁有者的每個存取資料庫，依擁有者。  
  
```  
SELECT DatabaseName, FileOwner  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileOwner;  
```  
  
### <a name="which-databases-contain-the-same-tables"></a>資料庫包含相同的資料表？  
下列查詢會使用子查詢來尋找所有出現在清單中的資料表，一次以上的資料表名稱，然後會使用這份資料表取得的資料庫名稱。 結果會傳回做為資料庫名稱，然後在資料表名稱，且會依照資料表名稱。  
  
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
  
### <a name="which-databases-were-not-modified-in-the-last-six-months"></a>過去六個月內未經修改的資料庫？  
下列查詢會取得目前的日期，取得六個月前的月份值，然後傳回具有大於六個月以前的修改日期的資料庫清單。  
  
```  
SELECT DatabaseName, DateModified  
FROM dbo.SSMA_Access_InventoryDatabases  
WHERE DATEDIFF(month, DateModified, GETDATE()) > 6  
ORDER BY DateModified;  
```  
  
### <a name="which-databases-contain-private-information"></a>資料庫包含個人資訊？  
Access 資料庫可能包含機密或個人資訊。 您可能想要移動這些資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]利用其安全性功能。 如果您知道包含機密資料的資料行具有特定名稱，或包含特定的字元，您可以使用查詢來尋找包含該資訊的所有資料行。 例如，您可以找到所有資料行包含字串 「 薪資 」。  然後查詢會傳回資料庫名稱、 資料表名稱，以及資料行名稱。  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D. DatabaseId  
WHERE ColumnName LIKE '%salary%';  
```  
如果您不知道資料行名稱，您可以撰寫查詢來傳回所有資料行。 若要這樣做，請從上一個查詢移除 WHERE 子句。  
  
## <a name="see-also"></a>另請參閱  
[準備移轉的 Access 資料庫](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  

