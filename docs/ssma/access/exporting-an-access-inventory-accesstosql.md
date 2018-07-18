---
title: 匯出 Access 清查 (AccessToSQL) |Microsoft 文件
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: 8a6c94a1335c8ee20aa7f42e179cd924b6661f55
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980670"
---
# <a name="exporting-an-access-inventory-accesstosql"></a>匯出 Access 清查 (AccessToSQL)
如果您有多個存取資料庫，而且您不確定要將移轉至哪些[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您可以匯出專案中的所有存取資料庫的詳細目錄。 您可以檢閱，然後查詢庫存中繼資料，以判斷哪一個資料庫和那些要移轉的資料庫內的物件。 此清查可讓您快速尋找解答，如下所示：  
  
-   最大的資料庫有哪些？  
  
-   大部分的資料庫擁有者是誰？  
  
-   資料庫包含相同的資料表？  
  
-   過去六個月內尚未經過修改的資料庫？  
  
-   資料庫包含私人資訊？  
  
在本主題結尾處提供可用來回答這些問題的查詢範例。  
  
## <a name="exported-metadata"></a>匯出的中繼資料  
SSMA 會將匯出存取資料庫、 資料表、 資料行、 索引、 外部索引鍵、 查詢、 報告、 表單、 巨集和模組的相關中繼資料。 每個項目分類的相關中繼資料匯出至個別的資料表。 針對這些資料表的結構描述，請參閱[Access 清查結構描述](http://msdn.microsoft.com/fdd3cff2-4d62-4395-8acf-71ea8f17f524)。  
  
## <a name="exporting-inventory-data"></a>匯出的清查資料  
若要匯出 Access 清查，您必須第一次開啟或建立 SSMA 專案，然後再加入 您想要分析的 Access 資料庫。 您將資料庫新增至 SSMA 專案之後，您會匯出這些資料庫的相關中繼資料指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫和結構描述。 如有必要，SSMA 會建立資料表來儲存的中繼資料。 SSMA，然後將 Access 資料庫的相關中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。  
  
> [!NOTE]  
> Access 資料庫可以分成多個檔案： 包含資料表和包含查詢、 表單、 報表、 巨集、 模組和快速鍵的前端資料庫後端資料庫。 如果您想要分割資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，加入 SSMA 中的前端資料庫。  
  
下面的指示說明如何建立專案、 將資料庫新增至專案、 連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，然後將匯出的清查資料。  
  
**若要建立專案**  
  
1.  開啟 SSMA for Access。  
  
2.  在 [檔案] 功能表上，選取 [新增專案]。  
  
    [新增專案]  對話方塊隨即出現。  
  
3.  在 **名稱**方塊中，輸入您專案的名稱。  
  
4.  在**位置**方塊中，輸入或選取專案的資料夾。  
  
5.  在 **移轉至**下拉式方塊中，選取您想要移轉，然後按一下目標版本**確定**。  
  
如需建立專案的詳細資訊，請參閱[Creating and Managing Projects](http://msdn.microsoft.com/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7)。  
  
**若要找出並新增資料庫**  
  
1.  在 **檔案**功能表上，按一下**尋找資料庫**。  
  
2.  在 [尋找資料庫精靈] 中，輸入磁碟機、 檔案路徑或您想要搜尋的 UNC 路徑。 或者，按一下**瀏覽**選取磁碟機或網路資料夾。  
  
3.  按一下 **新增**將位置新增至清單方塊。  
  
    重複前兩個步驟，來新增其他搜尋位置。  
  
4.  （選擇性） 加入搜尋準則，來調整資料庫所傳回的清單。  
  
    > [!IMPORTANT]  
    > **全部或部份檔案名稱**文字方塊中不支援萬用字元。  
  
5.  按一下 **掃描**。  
  
    掃描頁面隨即出現。 這會顯示找到的資料庫和搜尋進度。 若要停止搜尋，請按一下**停止**。  
  
6.  在 [選取檔案] 頁面中，選取您想要新增至專案的每個資料庫。  
  
    您可以使用**全選**並**全部清除**来選取或清除所有資料庫的清單頂端的按鈕。 您也可以按住 CTRL 鍵以選取多個資料列，或按住 SHIFT 鍵，向下選取的資料列範圍。  
  
7.  按 [下一步] 。  
  
8.  在 確認 頁面中，按一下 **完成**。  
  
如需有關將資料庫加入至專案的詳細資訊，請參閱 <<c0> [ 加入和移除的 Access 資料庫檔案](http://msdn.microsoft.com/e944c740-4c8a-4bc1-b0ed-be57bc06dced)。  
  
**若要連接到 SQL Server**  
  
1.  在 **檔案**功能表上，選取**連接到 SQL Server**。  
  
2.  在 [連線] 對話方塊中，輸入或選取的執行個體名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
    -   如果您要連接到本機電腦上的預設執行個體，您可以輸入**localhost**或句點 (**。**)。  
  
    -   如果您要連接到另一部電腦上的預設執行個體，請輸入電腦的名稱。  
  
    -   如果您要連接到具名執行個體，請輸入電腦名稱、 反斜線和執行個體名稱。 例如： MyServer\MyInstance。  
  
3.  在 **資料庫**方塊中，輸入匯出的中繼資料的目標資料庫的名稱。  
  
4.  如果您的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]設定為在非預設連接埠上接受連線中，輸入用於連接埠號碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中的連線**伺服器連接埠** 方塊中。 預設執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，預設連接埠號碼為 1433年。 具名執行個體，SSMA 會嘗試取得連接埠號碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]瀏覽器服務。  
  
5.  在 **驗證**下拉式選單中，選取要用於連線的驗證類型。 若要使用目前的 Windows 帳戶，請選取**Windows 驗證**。 若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登入，選取**SQL Server 驗證**，然後提供 使用者名稱和密碼。  
  
如需有關連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，請參閱 <<c2> [ 連接到 SQL Server &#40;AccessToSQL&#41;](../../ssma/access/connecting-to-sql-server-accesstosql.md)。</c2>  
  
**若要匯出的清查資訊**  
  
1.  在存取中繼資料總管 中，依序展開**存取 metabase**。  
  
2.  選取此核取方塊旁**資料庫**。  
  
    若要省略個別資料庫或資料庫物件，依序展開**資料庫**資料夾，然後再清除的資料庫或資料庫物件旁邊的核取方塊。  
  
3.  以滑鼠右鍵按一下**資料庫**，然後選取**匯出的結構描述**。  
  
4.  在 [**匯出選取的結構描述**] 對話方塊中，選取匯出的中繼資料，目標結構描述，然後按一下**確定**。  
  
匯出中繼資料，每次 SSMA 會將資料附加到清查。 無法更新或刪除現有的資料，在清查中。  
  
## <a name="querying-the-exported-metadata"></a>查詢之匯出的中繼資料  
匯出 Access 資料庫的相關中繼資料之後，您可以查詢中繼資料。 下面的指示說明使用中的 [查詢編輯器] 視窗[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]來執行查詢。  
  
**若要查詢的中繼資料**  
  
1.  從**開始**功能表上，指向**所有程式**，指向**Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005年**上，或者**Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008**上，或者**Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012年**，然後按一下**SQL Server Management Studio**。  
  
2.  在 [**連接到伺服器**] 對話方塊中，確認 [設定]，然後按一下**Connect**。  
  
3.  在 Management Studio 工具列中，按一下**新的查詢**開啟查詢編輯器。  
  
4.  在 [查詢編輯器] 視窗中，輸入查詢。 在下一節中，會顯示一些範例。  
  
5.  按下 F5 鍵以執行查詢。  
  
## <a name="query-examples"></a>查詢範例  
執行下列查詢之前，您應該執行 USE *database_name*先確定查詢會針對包含匯出的中繼資料的資料庫執行查詢。 例如，如果您的中繼資料匯出至名為 MyAccessMetadata 的資料庫時，您會新增下列開頭[!INCLUDE[tsql](../../includes/tsql_md.md)]程式碼：  
  
```  
USE MyAccessMetadata;  
GO  
```  
下列範例都會使用**dbo**結構描述。 如果您的中繼資料匯出至另一個結構描述時，請務必變更結構描述，當您執行這些查詢。  
  
### <a name="what-tables-and-columns-are-in-these-databases"></a>有哪些資料表和資料行？ 這些資料庫中  
下列查詢會聯結資料表包含資料行、 資料表和資料庫中繼資料，並接著會傳回所有的資料庫、 資料表和資料行，排序資料行名稱的名稱：  
  
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
下列查詢會傳回資料庫名稱、 檔案大小和數目的資料表在每個存取資料庫中，依檔案大小加以排序：  
  
```  
SELECT DatabaseName, FileSize, TablesCount  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileSize DESC;  
```  
  
### <a name="who-is-the-owner-of-most-of-the-databases"></a>大部分的資料庫的擁有者是誰？  
下列查詢會傳回資料庫名稱和擁有者的每個存取資料庫，依擁有人排序。  
  
```  
SELECT DatabaseName, FileOwner  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileOwner;  
```  
  
### <a name="which-databases-contain-the-same-tables"></a>資料庫包含相同的資料表？  
下列查詢會使用子查詢來尋找所有出現在清單中的資料表，一次以上的資料表名稱，並接著使用這份資料表取得的資料庫名稱。 結果會傳回做為資料庫名稱，然後在資料表名稱，且會依照資料表名稱。  
  
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
下列查詢會取得目前的日期、 月份值取得六個月前，並接著會傳回一份已修改的日期超過六個月前的資料庫。  
  
```  
SELECT DatabaseName, DateModified  
FROM dbo.SSMA_Access_InventoryDatabases  
WHERE DATEDIFF(month, DateModified, GETDATE()) > 6  
ORDER BY DateModified;  
```  
  
### <a name="which-databases-contain-private-information"></a>資料庫包含私人資訊？  
Access 資料庫可能包含機密或個人資訊。 您可能想要移動這些資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]善用它的安全性功能。 如果您知道包含機密資料的資料行具有特定名稱，或包含特定的字元，您可以使用查詢來尋找包含該資訊的所有資料行。 例如，您可以找到所有的資料行包含字串 「 薪資 」。  然後查詢會傳回資料庫名稱、 資料表名稱和資料行名稱。  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D. DatabaseId  
WHERE ColumnName LIKE '%salary%';  
```  
如果您不知道資料行名稱，您可以撰寫查詢以傳回所有資料行。 若要這樣做，請從上一個查詢中移除 WHERE 子句。  
  
## <a name="see-also"></a>另請參閱  
[準備移轉的 Access 資料庫](http://msdn.microsoft.com/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  
