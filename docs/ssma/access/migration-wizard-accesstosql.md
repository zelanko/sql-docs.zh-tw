---
title: 遷移 Wizard （AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migration Wizard dialog box
- Migration Wizard, adding Access databases
- Migration Wizard, Connect to SQL Azure
- Migration Wizard, Connect to SQL Server
- Migration Wizard, Link Tables
- Migration Wizard, Migration status
- Migration Wizard, New Project
- Migration Wizard, Selecting objects to migrate
ms.assetid: 5bab5914-b2ae-4795-8cf5-83e42d64bef2
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 658487186924fe5547edee70425524b2b4e3be6c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68083596"
---
# <a name="migration-wizard-accesstosql"></a>遷移 Wizard （AccessToSQL）
「遷移」嚮導會引導您完成從存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 遷移一或多個資料庫的工作。 藉由使用 wizard，您將建立專案、將資料庫新增至專案、選取要遷移的物件，以及連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 您也會轉換、載入和遷移存取架構和資料。 （選擇性）您可以將存取資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連結到或 SQL Azure 資料表。  
  
大部分的「遷移嚮導」頁面包含與現有 SSMA 對話方塊相同的選項。 因此，這裡描述的是 wizard 頁面，接著會提供連結，讓您可以深入瞭解個別選項。 如果頁面包含唯一的選項，則會記載在這裡。  
  
## <a name="starting-the-migration-wizard"></a>正在啟動遷移嚮導  
根據預設，當您開始 SSMA 時，會顯示 [遷移嚮導]。 您也可以選取 [**遷移嚮導**] **，在 [檔案] 功能表上**啟動精靈。  
  
## <a name="welcome-page"></a>歡迎頁面  
[歡迎使用] 頁面會介紹 [遷移嚮導]，並提供下列選項來啟動精靈。  
  
**在啟動時啟動此嚮導。**  
根據預設，SSMA 會在您開始 SSMA 時啟動 [遷移嚮導]。 若要防止自動啟動嚮導，請清除此核取方塊。  
  
## <a name="create-new-project-page"></a>[建立新專案] 頁面  
[建立新專案] 頁面是您在其中輸入 [專案檔名稱]、[位置] 和 [遷移] 專案類型（用來進行遷移的目標 SQL Server 版本）的位置。 如需詳細資訊，請參閱[新增專案（SSMA）](https://msdn.microsoft.com/ca294f6d-eeb5-42ca-9306-156281a3f0f3)  
  
## <a name="add-access-databases-page"></a>[加入 Access 資料庫] 頁面  
[新增存取資料庫] 頁面可讓您將一個或多個 Access 資料庫新增至專案。 您可以按一下 [**新增資料庫**] 來新增個別的資料庫，然後從**開啟**的視窗中選取資料庫。 或者，您可以使用 [**尋找資料庫**] 按鈕來尋找資料庫。 如需詳細資訊，請參閱下列主題：  
  
-   [新增和移除 Access 資料庫檔案](adding-and-removing-access-database-files-accesstosql.md)  
  
-   [尋找資料庫 Wizard （選取位置）](https://msdn.microsoft.com/00b2d32a-998b-47a7-b25c-589b5bd6777a)  
  
-   [尋找資料庫 Wizard （選取檔案）](https://msdn.microsoft.com/2f574a34-4bab-40a4-89a8-ad4907ffc3fd)  
  
-   [尋找資料庫精靈 (驗證選取項目)](https://msdn.microsoft.com/62e20e03-50cc-4ac8-8072-524d194d2ec3)  
  
## <a name="select-objects-to-migrate-page"></a>選取要遷移的物件頁面  
在 [選取要遷移的物件] 頁面上，選取要轉換的物件。 您可以選取所有物件、物件群組或個別物件。  
  
**若要選取物件**  
  
1.  展開 [**存取-元資料庫**]，然後展開 [**資料庫**]。  
  
2.  請進行下列任一或多項操作：  
  
    -   若要轉換所有資料庫，請選取 [**資料庫**] 旁的核取方塊。  
  
    -   若要轉換或省略個別資料庫，請選取或清除資料庫名稱旁邊的核取方塊。  
  
    -   若要轉換或省略查詢，請展開資料庫，然後選取或清除 [**查詢**] 核取方塊。  
  
    -   若要轉換或省略個別資料表，請展開資料庫，展開 [**資料表**]，然後選取或清除資料表旁的核取方塊。  
  
如果您有許多物件，您可能會想要使用右窗格中的 [**高級物件選取範圍**] 選項來篩選 Access 資料庫物件。 例如，如果您選取左窗格中的 [**資料表**]，則可以在 [**篩選**] 方塊中輸入字串，以篩選資料表清單。 接著，您可以使用窗格頂端的按鈕來選取或清除已篩選的資料表以進行遷移。  
  
如需有關篩選的詳細資訊，請參閱 [[高級物件選取（SSMA 一般）](https://msdn.microsoft.com/f53b0c79-5473-410a-a0dc-d8f544f7a63c)] 的 [選項] 區段。  
  
## <a name="connect-to-sql-server-page"></a>連接到 SQL Server 頁面  
在 [連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ] 頁面上，您可以指定連接屬性，然後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連接到。 如需詳細資訊，請參閱[連接到 SQL Server](connect-to-sql-server-accesstosql.md)。
  
> [!IMPORTANT]  
> 連接成功之後，您將會遇到**連結資料表**頁面，其中有連結資料表的選項。 按 **[下一步]** ，開始進行遷移。  
  
## <a name="connect-to-sql-azure-page"></a>連接到 SQL Azure 頁面  
在 [連接到 SQL Azure] 頁面上，您可以指定連接屬性，然後連接到 SQL Azure。 若要建立新的 azure 資料庫，您可以使用 [按一下**流覽]** 按鈕上顯示的 [**建立 azure 資料庫**] 選項來執行此動作。 如需詳細資訊，請參閱[連接到 SQL Azure](connect-to-azure-sql-db-accesstosql.md)  
  
> [!IMPORTANT]  
> 連接成功之後，您將會遇到**連結資料表**頁面，其中有連結資料表的選項。 按一下 [連結] 頁面上的 **[下一步]** 按鈕，開始進行遷移。  
  
## <a name="link-tables-page"></a>連結資料表頁面  
[連結資料表] 頁面可讓您將原始的 Access 資料表連結[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到遷移或 SQL Azure 資料表。 連結資料表會修改您的 Access 資料庫，讓您的查詢、表單、報表和資料存取頁面使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料庫中的資料，而非 Access 資料庫中的資料。  
  
**連結資料表**  
選取 [**連結資料表]** 核取方塊，將存取資料表連結到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]遷移或 SQL Azure 資料表。 若要開始遷移，您應該按 **[下一步]** 按鈕。  
  
## <a name="migration-status-page"></a>[遷移狀態] 頁面  
[遷移狀態] 頁面會顯示將存取架構轉換為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 sql azure 架構、將已轉換的架構載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 sql azure，然後再遷移資料的進度。  
  
如需此頁面的詳細資訊，請參閱[轉換、載入和遷移](https://msdn.microsoft.com/4ec83e96-88a5-4b7b-8d5a-f3429d9a936b)  
  
## <a name="see-also"></a>另請參閱  
[使用 SQL Server 移轉小幫手存取 &#40;AccessToSQL 的消費者入門&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[使用者介面參考（存取）](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
