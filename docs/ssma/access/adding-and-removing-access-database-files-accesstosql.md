---
title: 新增和移除 Access 資料庫檔案 (AccessToSQL) |Microsoft Docs
description: 瞭解如何在 SSMA 專案中新增或移除 Access 資料庫，以將存取資料移轉至 SQL Server 或 Azure SQL Database。
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 12c51ce9a3b4bdd83a1d1c4c7295f2ff438bc707
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987714"
---
# <a name="adding-and-removing-access-database-files-accesstosql"></a>新增和移除 Access 資料庫檔案 (AccessToSQL) 
若要將存取資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure，您必須將一或多個 access 資料庫新增至 SSMA 專案。 這些資料庫必須是 Access 97 或更新版本。 如果您有來自較舊版本存取的資料庫，則必須將資料庫轉換為較新的版本。 若要這麼做，您必須先在 Access 97 或更新版本中開啟並儲存資料庫，然後再將它們新增至 SSMA。  
  
## <a name="what-happens-when-you-add-access-database-files"></a>當您新增 Access 資料庫檔案時，會發生什麼事？  
當您將 Access 資料庫加入至 SSMA 專案時，SSMA 會讀取資料庫中繼資料，然後將此中繼資料加入至專案檔。 此中繼資料會描述資料庫及其物件。 當 SSMA 將物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Sql azure 語法，以及將資料移轉至或 Sql azure 時，會使用中繼資料 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 您可以在 Access Metadata Explorer 中流覽此中繼資料，並查看個別資料庫物件的屬性。  
  
> [!NOTE]  
> Access 資料庫可以分割成多個檔案：包含資料表的後端資料庫，以及包含查詢、表單、報表、宏、模組和快速鍵的前端資料庫。 如果您想要將分割資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure，請將前端資料庫新增至 SSMA。  
  
## <a name="permissions-that-are-required-by-ssma"></a>SSMA 所需的許可權  
若要將 Access 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure，Users 群組和 Admin 使用者必須擁有管理許可權。 如需有關如何使用工作組保護來遷移資料庫的詳細資訊，請參閱 [準備 Access 資料庫以進行遷移](preparing-access-databases-for-migration-accesstosql.md)。  
  
## <a name="selecting-databases-to-add"></a>選取要新增的資料庫  
如果您想要將一或多個資料庫加入至 SSMA 專案，而且檔案全都位於一個已知位置，您可以使用下列程式來新增檔案。  
  
**新增個別的資料庫檔案**  
  
1.  **在 [檔案**] 功能表上，按一下 [**新增資料庫**]。  
  
2.  在 [ **開啟** ] 對話方塊中，找出包含資料庫檔案的資料夾。  
  
3.  選取您要新增的檔案，然後按一下 [ **開啟**]。  
  
## <a name="finding-databases-to-add"></a>尋找要新增的資料庫  
如果您想要將多個 Access 資料庫從不同的資料夾加入至 SSMA 專案，或您想要新增單一檔案，但需要尋找檔案，您可以遵循下列步驟來找出其中一個檔案，然後將它們新增至專案。  
  
**尋找和新增資料庫**  
  
1.  **在 [檔案**] 功能表上，按一下 [**尋找資料庫**]。  
  
2.  在 [尋找資料庫] 嚮導中，輸入您要搜尋之磁片磁碟機的名稱、檔案路徑或 UNC 路徑。 或者，按一下 **[流覽]** 以找出磁片磁碟機或網路資料夾。  
  
3.  按一下 [ **新增** ]，將位置新增至清單。  
  
    重複上述兩個步驟，以新增更多搜尋位置。  
  
4.  （選擇性）加入搜尋條件，以精簡傳回的資料庫清單。  
  
    > [!IMPORTANT]  
    > [ **全部或部分的檔案名** ] 文字方塊不支援萬用字元。  
  
5.  按一下 [ **掃描**]。  
  
    [掃描] 頁面隨即出現。 這會顯示已找到的資料庫以及搜尋的進度。 若要停止搜尋，請按一下 [ **停止**]。  
  
6.  在 [選取檔案] 頁面上，選取您要加入至專案的資料庫。  
  
    您可以使用清單頂端的 [全 **選** ] 和 [ **全部清除** ] 按鈕，以選取或清除所有資料庫。 您可以按住 CTRL 鍵以選取多個資料庫，或按住 SHIFT 鍵來選取某個範圍的資料庫。  
  
7.  按一下 [下一步]。  
  
8.  在 [驗證] 頁面上，按一下 **[完成]**。  
  
## <a name="browsing-access-metadata"></a>流覽存取中繼資料  
將 Access 資料庫新增至專案之後，專案中繼資料會出現在 Access Metadata Explorer 中。 您可以在 explorer 中流覽資料庫和資料庫物件的階層架構。  
  
**流覽中繼資料**  
  
1.  在 [Access Metadata Explorer] 中，展開 [ **存取-元**資料]，然後展開 [ **資料庫**]。  
  
2.  展開您想要檢查的資料庫，然後展開 [ **查詢**]。  
  
    請注意查詢清單。 如果您選取查詢，右窗格中會顯示 **[SQL** ] 索引標籤和 [ **屬性** ] 索引標籤。  
  
3.  展開 [ **資料表]** ，然後選取資料表。  
  
    請注意，會出現四個索引標籤： **資料表**、 **類型對應**、 **屬性**和 **資料**。  
  
4.  展開 [資料表]，展開 [索引 **鍵**]，然後選取索引鍵。  
  
    索引鍵屬性會出現在右窗格中。  
  
5.  展開 [ **索引**]，然後選取索引。  
  
    索引屬性會出現在右窗格中。  
  
## <a name="refreshing-databases"></a>重新整理資料庫  
如果 Access 資料庫在您新增其檔案之後變更，您可以從 Access 資料庫更新中繼資料。  
  
**更新存取中繼資料**  
  
-   在 [Access Metadata Explorer] 中，以滑鼠右鍵按一下資料庫，然後選取 [ **從資料庫**重新整理]。  
  
## <a name="removing-databases"></a>移除資料庫  
您可以依照下列步驟，從專案中移除存取資料庫。  
  
**若要從專案中移除資料庫**  
  
1.  在 [Access Metadata Explorer] 中，展開 [ **存取-元**資料]，然後展開 [ **資料庫**]。  
  
2.  以滑鼠右鍵按一下資料庫，然後選取 [ **移除資料庫**]。  
  
## <a name="next-step"></a>後續步驟  
遷移程式的下一個步驟是 [連接到 SQL Server](../sybase/connecting-to-sql-server-sybasetosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[建立及管理專案](creating-and-managing-projects-accesstosql.md)  
