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
ms.openlocfilehash: 597de64479014e44f38c7073b6bc88e76a3137b4
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934129"
---
# <a name="adding-and-removing-access-database-files-accesstosql"></a>新增和移除 Access 資料庫檔案 (AccessToSQL) 
若要將存取資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure，您必須將一或多個 access 資料庫新增至 SSMA 專案。 這些資料庫必須是 Access 97 或更新版本。 如果您有舊版 Access 的資料庫，則必須將資料庫轉換成較新的版本。 若要這麼做，您可以開啟並儲存 Access 97 或更新版本中的資料庫，然後再將它們新增至 SSMA。  
  
## <a name="what-happens-when-you-add-access-database-files"></a>當您新增 Access 資料庫檔案時，會發生什麼事？  
當您將 Access 資料庫新增至 SSMA 專案時，SSMA 會讀取資料庫中繼資料，然後將此中繼資料加入至專案檔。 此中繼資料會描述資料庫及其物件。 SSMA 會在將物件轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Sql azure 語法，以及將資料移轉至或 Sql azure 時，使用中繼資料 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 您可以在 [存取中繼資料瀏覽器] 中流覽此中繼資料，並查看個別資料庫物件的屬性。  
  
> [!NOTE]  
> Access 資料庫可以分割成多個檔案：包含資料表的後端資料庫，以及包含查詢、表單、報表、宏、模組和快捷方式的前端資料庫。 如果您想要將分割資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure，請將前端資料庫新增至 SSMA。  
  
## <a name="permissions-that-are-required-by-ssma"></a>SSMA 所需的許可權  
若要將 Access 資料庫移轉到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure，Users 群組和 Admin 使用者必須具有 [管理] 許可權。 如需如何使用工作組保護來遷移資料庫的相關資訊，請參閱[準備 Access 資料庫以進行遷移](preparing-access-databases-for-migration-accesstosql.md)。  
  
## <a name="selecting-databases-to-add"></a>選取要新增的資料庫  
如果您想要將一個或多個資料庫新增至 SSMA 專案，而且檔案全都位於一個已知位置，您可以使用下列程式來新增檔案。  
  
**若要加入個別的資料庫檔案**  
  
1.  **在 [檔案**] 功能表上，按一下 [**新增資料庫**]。  
  
2.  在 [**開啟**] 對話方塊中，找出包含資料庫檔案的資料夾。  
  
3.  選取您要新增的檔案，然後按一下 [**開啟**]。  
  
## <a name="finding-databases-to-add"></a>尋找要新增的資料庫  
如果您想要將多個 Access 資料庫從不同的資料夾新增至 SSMA 專案，或者您想要新增單一檔案但必須尋找檔案，您可以遵循下列步驟找出其中一個檔案，並將它們加入至專案。  
  
**尋找並新增資料庫**  
  
1.  **在 [檔案**] 功能表上，按一下 [**尋找資料庫**]。  
  
2.  在 [尋找資料庫] 中，輸入要搜尋的磁片磁碟機名稱、檔案路徑或 UNC 路徑。 或者，按一下 **[流覽]** 以找出磁片磁碟機或網路資料夾。  
  
3.  按一下 [**新增**]，將位置加入清單中。  
  
    重複前兩個步驟，以新增更多搜尋位置。  
  
4.  （選擇性）加入搜尋條件，以精簡傳回的資料庫清單。  
  
    > [!IMPORTANT]  
    > **[全部] 或 [部分] 的 [檔案名**] 文字方塊不支援萬用字元。  
  
5.  按一下 [**掃描**]。  
  
    [掃描] 頁面隨即出現。 這會顯示已找到的資料庫和搜尋的進度。 若要停止搜尋，請按一下 [**停止**]。  
  
6.  在 [選取檔案] 頁面上，選取您想要加入至專案的資料庫。  
  
    您可以使用清單頂端的 [**全選**] 和 [**全部清除**] 按鈕來選取或清除所有資料庫。 您可以按住 CTRL 鍵來選取多個資料庫，或按住 SHIFT 鍵來選取某個範圍的資料庫。  
  
7.  按 [下一步]  。  
  
8.  在 [驗證] 頁面上，按一下 **[完成]**。  
  
## <a name="browsing-access-metadata"></a>流覽存取中繼資料  
將 Access 資料庫新增至專案之後，專案中繼資料就會出現在 [存取中繼資料 Explorer] 中。 您可以在 explorer 中流覽資料庫和資料庫物件的階層架構。  
  
**流覽中繼資料**  
  
1.  在 [存取中繼資料瀏覽器] 中，展開 [**存取-資料庫**]，然後展開 [**資料庫**]。  
  
2.  展開您要檢查的資料庫，然後展開 [**查詢**]。  
  
    請注意查詢清單。 如果您選取查詢，右窗格中會出現 **[SQL** ] 索引標籤和 [**屬性**] 索引標籤。  
  
3.  展開 [**資料表]** ，然後選取資料表。  
  
    請注意，會出現四個索引標籤：**資料表**、**類型對應**、**屬性**和**資料**。  
  
4.  依序展開資料表和 [索引**鍵**]，然後選取索引鍵。  
  
    索引鍵屬性會出現在右窗格中。  
  
5.  展開 [**索引**]，然後選取索引。  
  
    索引屬性會出現在右窗格中。  
  
## <a name="refreshing-databases"></a>重新整理資料庫  
如果 Access 資料庫在您新增其檔案之後變更，您可以從 Access 資料庫更新中繼資料。  
  
**更新存取中繼資料**  
  
-   在 [存取中繼資料 Explorer] 中，以滑鼠右鍵按一下資料庫，然後選取 [**從資料庫**重新整理]。  
  
## <a name="removing-databases"></a>移除資料庫  
您可以遵循下列步驟，從專案中移除 Access 資料庫。  
  
**若要從專案中移除資料庫**  
  
1.  在 [存取中繼資料瀏覽器] 中，展開 [**存取-資料庫**]，然後展開 [**資料庫**]。  
  
2.  以滑鼠右鍵按一下資料庫，然後選取 [**移除資料庫**]。  
  
## <a name="next-step"></a>後續步驟  
遷移程式的下一個步驟是[連接到 SQL Server](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[建立及管理專案](creating-and-managing-projects-accesstosql.md)  
  
