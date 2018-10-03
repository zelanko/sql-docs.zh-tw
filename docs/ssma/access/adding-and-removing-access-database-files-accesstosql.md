---
title: 新增和移除存取資料庫檔案 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- adding Access files
- adding and removing Access databases
- browsing Access metadata
- browsing metadata, Access databases
- connecting, Access databases
- databases
- files, adding and removing
- finding Access databases
- finding database files
- locating database files
- metadata
- metadata, browsing
- metadata, refreshing
- refreshing metadata
- removing Access files
- scanning for database files
- searching for database files
ms.assetid: e944c740-4c8a-4bc1-b0ed-be57bc06dced
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2ec65ffa5ee5df74d48de5280fedb825da8607aa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47598157"
---
# <a name="adding-and-removing-access-database-files-accesstosql"></a>新增和移除 Access 資料庫檔案 (AccessToSQL)
若要將 Access 資料移至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，您必須將一或多個 Access 資料庫加入 SSMA 專案。 這些資料庫必須是 Access 97 或更新版本。 如果您的資料庫從舊版的存取權，您必須將資料庫轉換為較新版本。 您可以開啟和儲存在 Access 97 或更新版本的資料庫，才將它們新增至 SSMA。  
  
## <a name="what-happens-when-you-add-access-database-files"></a>當您新增 Access 資料庫檔案時，會發生什麼事？  
當您新增至 SSMA 專案的 Access 資料庫時，SSMA 讀取資料庫中繼資料，然後將此中繼資料新增至專案檔。 此中繼資料描述資料庫和其物件。 SSMA 會將轉換物件時，會使用中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 的語法，以及當它將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 您可以瀏覽此存取中繼資料總管 中的中繼資料，然後檢閱個別的資料庫物件的屬性。  
  
> [!NOTE]  
> Access 資料庫可以分成多個檔案： 包含資料表的後端資料庫和包含查詢、 表單、 報表、 巨集、 模組和快速鍵的前端資料庫。 如果您想要分割資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，加入 SSMA 中的前端資料庫。  
  
## <a name="permissions-that-are-required-by-ssma"></a>SSMA 所需的權限  
若要存取將資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure、 使用者群組和系統管理員使用者必須具有管理員權限。 如需如何移轉工作群組保護的資料庫資訊，請參閱[準備移轉的 Access 資料庫](preparing-access-databases-for-migration-accesstosql.md)。  
  
## <a name="selecting-databases-to-add"></a>選取要新增的資料庫  
如果您想要將一或多個資料庫新增至 SSMA 專案，而且全都放在一個已知的位置是檔案，您可以使用下列程序來新增檔案。  
  
**若要新增個別的資料庫檔案**  
  
1.  在 **檔案**功能表上，按一下**新增資料庫**。  
  
2.  在 **開啟**對話方塊方塊中，找出包含資料庫或多個檔案的資料夾。  
  
3.  選取您要新增，然後按一下 [檔案]**開啟**。  
  
## <a name="finding-databases-to-add"></a>尋找要新增的資料庫  
如果您想要將多個存取資料庫從不同的資料夾新增至 SSMA 專案，或您想要新增單一檔案，但必須尋找檔案，您可以依照下列步驟來找出其中一個更多檔案，並將其新增至專案。  
  
**若要找出並新增資料庫**  
  
1.  在 **檔案**功能表上，按一下**尋找資料庫**。  
  
2.  在 [尋找資料庫精靈] 中，輸入磁碟機、 檔案路徑或您想要搜尋的 UNC 路徑的名稱。 或者，按一下**瀏覽**找出磁碟機或網路資料夾。  
  
3.  按一下 **新增**將位置新增至清單。  
  
    重複前兩個步驟，以新增更多的搜尋位置。  
  
4.  （選擇性） 加入搜尋準則，來調整資料庫所傳回的清單。  
  
    > [!IMPORTANT]  
    > **全部或部份檔案名稱**文字方塊中不支援萬用字元。  
  
5.  按一下 **掃描**。  
  
    掃描頁面隨即出現。 這會顯示找到的資料庫和搜尋的進度。 若要停止搜尋，請按一下**停止**。  
  
6.  在 [選取檔案] 頁面中，選取您想要新增至專案的資料庫。  
  
    您可以使用**全選**並**全部清除**来選取或清除所有資料庫的清單頂端的按鈕。 您可以按住 CTRL 鍵以選取多個資料庫，或按住 SHIFT 鍵，向下選取範圍的資料庫。  
  
7.  按 [下一步] 。  
  
8.  在 確認 頁面中，按一下 **完成**。  
  
## <a name="browsing-access-metadata"></a>瀏覽存取中繼資料  
Access 資料庫加入至專案之後，專案中繼資料會出現在存取中繼資料總管 中。 您可以瀏覽資料庫與 [總管] 中的資料庫物件的階層。  
  
**若要瀏覽中繼資料**  
  
1.  在存取中繼資料總管 中，依序展開**存取 metabase**，然後展開**資料庫**。  
  
2.  展開您想要檢閱，然後再展開的資料庫**查詢**。  
  
    請注意，查詢的清單。 如果您選取查詢時， **SQL**索引標籤和**屬性** 索引標籤會顯示在右窗格中。  
  
3.  依序展開**資料表**，然後選取資料表。  
  
    請注意，會出現四個索引標籤：**資料表**，**型別對應**，**屬性**，以及**資料**。  
  
4.  展開資料表，再展開**金鑰**，然後選取 索引鍵。  
  
    索引鍵的屬性會出現在右窗格中。  
  
5.  依序展開**索引**，然後選取 索引。  
  
    索引屬性會出現在右窗格中。  
  
## <a name="refreshing-databases"></a>重新整理資料庫  
如果您將新增其檔案之後，就會變更的 Access 資料庫，您可以更新從 Access 資料庫的中繼資料。  
  
**若要更新存取中繼資料**  
  
-   在存取中繼資料總管，以滑鼠右鍵按一下資料庫，然後按**從資料庫重新整理**。  
  
## <a name="removing-databases"></a>移除資料庫  
您可以遵循下列步驟，從專案移除的 Access 資料庫。  
  
**若要從專案移除資料庫**  
  
1.  在存取中繼資料總管 中，依序展開**存取 metabase**，然後展開**資料庫**。  
  
2.  以滑鼠右鍵按一下資料庫，然後按**Remove Database**。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[連接到 SQL Server](http://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[建立和管理專案](creating-and-managing-projects-accesstosql.md)  
  
