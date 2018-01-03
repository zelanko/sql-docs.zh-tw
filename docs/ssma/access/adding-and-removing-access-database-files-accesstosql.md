---
title: "加入和移除存取資料庫檔案 (AccessToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: "15"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 64e1bc5dd6b78df1f24ee03b65cfdf6b796c0e39
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="adding-and-removing-access-database-files-accesstosql"></a>加入和移除 Access 資料庫檔案 (AccessToSQL)
若要存取將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，您必須加入一個或多個 Access 資料庫的 SSMA 專案。 這些資料庫必須 Access 97 或更新版本。 如果您的資料庫從舊版的存取權，您必須將資料庫轉換為較新版本。 您這麼做，開啟並儲存資料庫 Access 97 或更新版本中，您將它們加入 SSMA 之前。  
  
## <a name="what-happens-when-you-add-access-database-files"></a>當您將加入 Access 資料庫檔案發生什麼事？  
當您將 Access 資料庫中加入的 SSMA 專案時，SSMA 讀取資料庫中繼資料，然後將此中繼資料加入至專案檔。 此中繼資料描述資料庫及其物件。 SSMA 會轉換至的物件時，會使用中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的語法，以及當它能將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 您可以瀏覽存取中繼資料總管 在此中繼資料，然後檢閱個別的資料庫物件的屬性。  
  
> [!NOTE]  
> Access 資料庫可以分成多個檔案： 包含資料表，後端資料庫和包含查詢、 表單、 報表、 巨集、 模組和快速鍵的前端資料庫。 如果您想要分割資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中，加入 SSMA 的前端資料庫。  
  
## <a name="permissions-that-are-required-by-ssma"></a>SSMA 所需的權限  
若要存取將資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure、 使用者群組和系統管理員使用者必須具有管理權限。 如需如何移轉工作群組保護的資料庫資訊，請參閱[準備移轉的 Access 資料庫](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  
## <a name="selecting-databases-to-add"></a>選取要加入的資料庫  
如果您想要將一個或多個資料庫的 SSMA 專案，而且檔案都位於一個已知的位置，您可以使用下列程序來加入檔案。  
  
**若要加入個別的資料庫檔案**  
  
1.  在**檔案**功能表上，按一下 **加入資料庫**。  
  
2.  在**開啟**對話方塊方塊中，找出包含資料庫檔案的資料夾。  
  
3.  選取您想要新增，然後按一下 檔案**開啟**。  
  
## <a name="finding-databases-to-add"></a>尋找要加入的資料庫  
如果您想要從不同的資料夾的存取的多個資料庫加入至 SSMA 專案，或您想要新增單一檔案，但必須先找到檔案，您可以遵循下列步驟來尋找更多檔案，並將其新增至專案。  
  
**若要找出並新增資料庫**  
  
1.  在**檔案**功能表上，按一下 **尋找資料庫**。  
  
2.  在 [尋找資料庫精靈] 中，輸入磁碟機、 檔案路徑或您想要搜尋的 UNC 路徑的名稱。 或者，按一下**瀏覽**找出磁碟機或網路資料夾。  
  
3.  按一下**新增**將的位置加入至清單。  
  
    重複上述兩個步驟，並加入更多的搜尋位置。  
  
4.  或者，新增搜尋準則來調整資料庫所傳回的清單。  
  
    > [!IMPORTANT]  
    > **全部或部份檔案名稱**文字方塊中不支援萬用字元。  
  
5.  按一下**掃描**。  
  
    掃描頁面隨即出現。 這會顯示已找到資料庫和搜尋的進度。 若要停止搜尋，請按一下**停止**。  
  
6.  在 [選取檔案] 頁面中，選取您想要加入至專案的資料庫。  
  
    您可以使用**全選**和**全部清除**加以選取或清除所有的資料庫清單頂端的按鈕。 您可以按住 CTRL 鍵以選取多個資料庫，或按住 SHIFT 鍵向選取的資料庫的範圍。  
  
7.  按 [下一步] 。  
  
8.  在確認頁面上，按一下 **完成**。  
  
## <a name="browsing-access-metadata"></a>瀏覽存取中繼資料  
您將 Access 資料庫加入至專案之後，專案中繼資料會出現在存取中繼資料總管 中。 您可以瀏覽資料庫和 [總管] 中的資料庫物件的階層。  
  
**若要瀏覽中繼資料**  
  
1.  在存取中繼資料總管，依序展開**存取 metabase**，然後展開**資料庫**。  
  
2.  展開您想要檢閱，然後展開資料庫**查詢**。  
  
    請注意查詢的清單。 如果您選取的查詢， **SQL**  索引標籤和**屬性**索引標籤會出現在右窗格中。  
  
3.  展開**資料表**，然後選取資料表。  
  
    請注意，會出現四個索引標籤：**資料表**，**類型對應**，**屬性**，和**資料**。  
  
4.  依序展開 資料表**金鑰**，然後選取 索引鍵。  
  
    索引鍵屬性會出現在右窗格中。  
  
5.  展開**索引**，然後選取索引。  
  
    索引屬性會出現在右窗格中。  
  
## <a name="refreshing-databases"></a>重新整理資料庫  
如果 Access 資料庫變更，將其檔案之後，您可以更新從 Access 資料庫的中繼資料。  
  
**若要更新存取中繼資料**  
  
-   在存取中繼資料總管，以滑鼠右鍵按一下資料庫，然後**從資料庫重新整理**。  
  
## <a name="removing-databases"></a>移除資料庫  
您可以依照下列步驟，從專案移除 Access 資料庫。  
  
**從專案移除資料庫**  
  
1.  在存取中繼資料總管，依序展開**存取 metabase**，然後展開**資料庫**。  
  
2.  以滑鼠右鍵按一下資料庫，然後選取**Remove Database**。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[連接到 SQL Server](http://msdn.microsoft.com/en-us/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)。  
  
## <a name="see-also"></a>請參閱  
[將 Access 資料庫移轉至 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[建立及管理專案](http://msdn.microsoft.com/en-us/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7)  
  
