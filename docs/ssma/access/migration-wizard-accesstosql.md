---
title: 移轉精靈 (AccessToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-access
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
- Migration Wizard dialog box
- Migration Wizard, adding Access databases
- Migration Wizard, Connect to SQL Azure
- Migration Wizard, Connect to SQL Server
- Migration Wizard, Link Tables
- Migration Wizard, Migration status
- Migration Wizard, New Project
- Migration Wizard, Selecting objects to migrate
ms.assetid: 5bab5914-b2ae-4795-8cf5-83e42d64bef2
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 356f06ec66e0fa18c0406f34ce706eae0eaf2886
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="migration-wizard-accesstosql"></a>移轉精靈 (AccessToSQL)
移轉精靈引導您完成移轉的一個或多個資料庫的存取權從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 使用精靈，您會建立專案、 將資料庫加入至專案，請選取要移轉，並連接到的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 您也將轉換、 載入及移轉存取結構描述和資料。 （選擇性） 您可以 Access 資料表連結至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的資料表。  
  
大部分移轉精靈頁面包含與現有的 SSMA 對話方塊相同的選項。 因此，此處描述的精靈頁面，以便您可以深入了解個別的選項，然後提供連結。 如果某個頁面包含唯一的選項，它們是在此處記錄。  
  
## <a name="starting-the-migration-wizard"></a>啟動移轉精靈  
根據預設，當您啟動 SSMA，會出現 「 移轉精靈 」。 您也可以在啟動精靈**檔案**功能表選取**移轉精靈**。  
  
## <a name="welcome-page"></a>歡迎頁面  
歡迎使用 頁面會介紹 「 移轉精靈 」，並提供下列選項來啟動精靈。  
  
**啟動在啟動此精靈。**  
根據預設，當您啟動 SSMA SSMA 時，會啟動移轉精靈。 若要避免自動啟動精靈，請清除此核取方塊。  
  
## <a name="create-new-project-page"></a>建立新的專案頁面  
建立新專案頁面是您在其中輸入專案的檔案名稱、 位置和移轉專案類型 （目標用於移轉的 SQL Server 的版本）。 如需詳細資訊，請參閱[新專案 (SSMA)](http://msdn.microsoft.com/en-us/ca294f6d-eeb5-42ca-9306-156281a3f0f3)  
  
## <a name="add-access-databases-page"></a>新增存取資料庫頁面  
加入 Access 資料庫頁面是您將一或多個 Access 資料庫加入至專案。 您可以新增個別的資料庫，依序按一下**加入資料庫**，然後選取 從資料庫**開啟**視窗。 或者，您可以藉由尋找資料庫**尋找資料庫** 按鈕。 如需詳細資訊，請參閱下列主題：  
  
-   [加入和移除 Access 資料庫檔案](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)  
  
-   [尋找資料庫精靈 （選取位置）](http://msdn.microsoft.com/en-us/00b2d32a-998b-47a7-b25c-589b5bd6777a)  
  
-   [尋找資料庫精靈 （選取檔案）](http://msdn.microsoft.com/en-us/2f574a34-4bab-40a4-89a8-ad4907ffc3fd)  
  
-   [尋找資料庫精靈 (驗證選取項目)](http://msdn.microsoft.com/en-us/62e20e03-50cc-4ac8-8072-524d194d2ec3)  
  
## <a name="select-objects-to-migrate-page"></a>選取要移轉的頁面物件  
在 [移轉] 頁面來選取物件，選取要轉換的物件。 您可以選取所有物件的物件或個別物件的群組。  
  
**若要選取物件**  
  
1.  展開**存取 metabase**，然後展開**資料庫**。  
  
2.  請進行下列任一或多項操作：  
  
    -   若要轉換的所有資料庫，選取核取方塊旁的 **資料庫**。  
  
    -   若要轉換或省略個別資料庫，選取或清除資料庫名稱旁邊的核取方塊。  
  
    -   轉換或省略查詢中，展開資料庫，然後選取或清除**查詢**核取方塊。  
  
    -   若要轉換或省略個別資料表中，展開資料庫，展開 **資料表**，然後選取或清除資料表旁的核取方塊。  
  
如果您有許多物件時，您可能想要使用**進階物件選取項目**右窗格中的選項來篩選存取資料庫物件。 例如，如果您選取**資料表**在左窗格中，您可以再篩選的資料表清單輸入字串中的**篩選**方塊。 然後，您可以選取或清除已篩選的資料表移轉為使用窗格頂端的按鈕。  
  
如需篩選的詳細資訊，請參閱 [選項] 區段的[（SSMA 通用） 的 進階物件選取](http://msdn.microsoft.com/en-us/f53b0c79-5473-410a-a0dc-d8f544f7a63c)。  
  
## <a name="connect-to-sql-server-page"></a>連接至 SQL Server 頁面  
在 [連線至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]] 頁面上，您指定連接屬性，然後連線至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如需詳細資訊，請參閱[連接到 SQL Server](http://msdn.microsoft.com/en-us/00e0432e-ec26-4ab4-af64-c9ca760e3541)  
  
> [!IMPORTANT]  
> 一旦連線成功，您將會遇到**連結資料表**其中您可以選擇連結資料表的頁面。 按一下**下一步**和移轉開始。  
  
## <a name="connect-to-sql-azure-page"></a>連接到 SQL Azure 的頁面  
在 [連接到 SQL Azure] 頁面中，您指定連接屬性，然後再連接到 SQL Azure。 若要建立新的 azure 資料庫，您可以使用**建立 Azure 資料庫**選項會出現在按**瀏覽** 按鈕。 如需詳細資訊，請參閱[連接到 SQL Azure](http://msdn.microsoft.com/en-us/bf44b236-d9be-41ae-a5fd-bd73038e505f)  
  
> [!IMPORTANT]  
> 一旦連線成功，您將會遇到**連結資料表**其中您可以選擇連結資料表的頁面。 按一下**下一步**啟動移轉 [連結] 頁面上的按鈕。  
  
## <a name="link-tables-page"></a>連結資料表 頁面  
[連結資料表] 頁面可讓您將原始的 Access 資料表連結至移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的資料表。 連結資料表，讓您查詢、 表單、 報表和資料存取頁面使用中的資料會修改您的 Access 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫，而非 Access 資料庫中的資料。  
  
**連結資料表**  
選取**連結資料表**核取方塊以 Access 資料表連結至已移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的資料表。 若要啟動的移轉，您應該按一下**下一步** 按鈕。  
  
## <a name="migration-status-page"></a>移轉 [狀態] 頁面  
[移轉狀態] 頁面中顯示的轉換來存取結構描述進度[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 結構描述，載入將已轉換的結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，然後將資料移轉。  
  
如需此頁面的詳細資訊，請參閱[轉換、 載入和移轉](http://msdn.microsoft.com/en-us/4ec83e96-88a5-4b7b-8d5a-f3429d9a936b)  
  
## <a name="see-also"></a>另請參閱  
[開始使用 SQL Server 移轉小幫手存取&#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[將 Access 資料庫移轉至 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[使用者介面 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
