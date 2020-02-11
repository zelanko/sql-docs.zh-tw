---
title: 建立和管理專案（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- creating projects
- new projects
- opening projects
- projects
- projects, creating and managing
- saving metadata
- saving projects
ms.assetid: f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: abbe0746193df3fe341b4f66086291dc1055e11b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006613"
---
# <a name="creating-and-managing-projects-accesstosql"></a>建立和管理專案（AccessToSQL）
若要將 Access 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]遷移到或 SQL Azure，您必須先建立 SSMA 專案。 專案是一個檔案，其中包含您想要遷移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 sql Azure 之 Access 資料庫的相關中繼資料、目標實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 sql azure 的相關中繼資料，將會接收遷移的物件和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料、連接資訊和專案設定。  
  
## <a name="reviewing-default-project-settings"></a>查看預設專案設定  
SSMA 包含數個用於轉換和同步處理資料庫物件，以及用於轉換資料的選項。 這些選項的預設設定適用于許多使用者。 不過，在建立新的 SSMA 專案之前，您應該先檢查選項，並視需要變更將用於所有新專案的預設設定。  
  
**若要查看預設專案設定**  
  
1.  在 [**工具**] 功能表上，選取 [**預設專案設定**]。  
  
2.  在 [**遷移目標版本**] 下拉式選中選取要查看/變更設定的專案類型，然後按一下 **[一般**] 索引標籤。  
  
3.  在左窗格中，按一下 [**轉換**]。  
  
4.  在右窗格中，檢查選項。 如需這些選項的詳細資訊，請參閱[專案設定（轉換）](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)。  
  
5.  視需要變更選項。  
  
6.  針對 [**遷移**]、[ **GUI**] 和 [**類型對應**] 頁面重複上述步驟。  
  
    -   如需有關遷移選項的詳細資訊，請參閱[專案設定（遷移）](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)。  
  
    -   如需使用者介面選項的詳細資訊，請參閱[專案設定（GUI）](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)。  
  
    -   如需資料類型對應設定的詳細資訊，請參閱[專案設定（類型對應）](https://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)。  
  
    -   如需 SQL Azure 設定的詳細資訊，請參閱[專案設定（Sql Azure）](https://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e)。  
  
**注意**只有當您在建立專案時選取 [遷移至 SQL Azure] 時，才會提供 SQL Azure 設定。  
  
## <a name="creating-new-projects"></a>建立新專案  
SSMA 會啟動，而不會載入預設專案。 若要將資料從 Access 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]遷移到或 SQL Azure，您必須建立專案。  
  
**建立新的專案**  
  
1.  在 [檔案]**** 功能表上，選取 [新增專案]****。  
  
    此時會出現 [新增專案]**** 對話方塊。  
  
2.  在 [**名稱**] 方塊中，輸入專案的名稱。  
  
3.  在 [**位置**] 方塊中，輸入或選取專案的資料夾  
  
4.  在 [遷移至] 下拉式選單中，選取 SQL Server 2005/SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016/Azure SQL DB 中的其中一個，然後按一下 **[確定]**。  
  
SSMA 會建立專案檔。 您現在可以執行[加入一個或多個 Access 資料庫](adding-and-removing-access-database-files-accesstosql.md)的下一個步驟。  
  
## <a name="customizing-project-settings"></a>自訂專案設定  
除了定義預設專案設定（適用于所有新的 SSMA 專案）之外，您也可以自訂每個專案的設定。 如需詳細資訊，請參閱[設定轉換和遷移選項](setting-conversion-and-migration-options-accesstosql.md)。  
  
當您自訂來源與目標資料庫之間的資料類型對應時，您可以在專案、資料庫或物件層級定義對應。 如需型別對應的詳細資訊，請參閱[對應來源和目標資料類型](mapping-source-and-target-data-types-accesstosql.md)。  
  
## <a name="saving-projects"></a>儲存專案  
當您儲存專案時，SSMA 會將專案設定和選擇性的資料庫中繼資料保存至專案檔。  
  
**儲存專案**  
  
-   **在 [檔案**] 功能表上，選取 [**儲存專案**]。  
  
    如果專案內的資料庫已變更或尚未轉換，SSMA 會提示您將中繼資料儲存到專案中。 儲存中繼資料可讓您離線工作。 此外，它也可讓您將完整的專案檔案傳送給其他人，包括技術支援人員。 如果系統提示您儲存中繼資料，請執行下列動作：  
  
    1.  針對顯示 [**中繼資料遺失**] 狀態的每個資料庫，選取資料庫名稱旁邊的核取方塊。  
  
        儲存中繼資料可能需要幾分鐘的時間。 如果您不想在此時儲存中繼資料，請不要選取任何核取方塊。  
  
    2.  按一下 [檔案]  。  
  
        SSMA 將會剖析存取架構，並將中繼資料儲存至專案檔。  
  
## <a name="opening-projects"></a>開啟專案  
當您開啟專案時，它會從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 中斷連接。 這可讓您離線工作。 若要將中繼資料載入資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]物件更新至或 SQL Azure。 若要遷移資料，您必須重新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連線到或 SQL Azure。  
  
**開啟專案**  
  
1.  您可以使用下列其中一個程序：  
  
    -   在 [檔案 **] 功能表上，指向 [** **最近使用的專案**]，然後選取您要開啟的專案。  
  
    -   在 [**檔案**] 功能表上，選取 [**開啟專案**]，找出 a2ssproj 專案檔案，選取檔案，然後按一下 [**開啟**]。  
  
2.  若要重新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連線到，請**在 [檔案**] 功能表上，選取 [重新連線**到 SQL Server**]。  
  
3.  若要重新連線到 SQL Azure，請**在 [檔案**] 功能表上，選取 [重新連線**到 sql azure]。**  
  
## <a name="next-step"></a>後續步驟  
遷移程式的下一個步驟是[加入一個或多個 Access 資料庫](adding-and-removing-access-database-files-accesstosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[新增和移除 Access 資料庫檔案](adding-and-removing-access-database-files-accesstosql.md)  
  
