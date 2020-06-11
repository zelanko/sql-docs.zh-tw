---
title: 連接到 SAP ASE （SybaseToSQL） |Microsoft Docs
description: 瞭解如何連接到調適型伺服器，將 SAP 調適型伺服器企業（ASE）資料庫移轉至 SQL Server 或 Azure SQL Database。
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to Sybase
ms.assetid: a45a2330-9175-4c9e-af38-ef920e350614
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 0558e86380c6cec822103a22b746b5af05437cae
ms.sourcegitcommit: 6593b3b6365283bb76c31102743cdccc175622fe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84306087"
---
# <a name="connecting-to-sap-ase-sybasetosql"></a>連接到 SAP ASE （SybaseToSQL）

若要將 SAP 調適型伺服器 Enterprise （ASE）資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure，您必須連接到包含您要遷移之資料庫的調適型伺服器。 當您連接時，SSMA 會取得調適型伺服器上所有資料庫的相關中繼資料，並在 [Sybase 中繼資料 Explorer] 窗格中顯示資料庫中繼資料。 SSMA 會儲存資料庫伺服器的相關資訊，但不會儲存密碼。  
  
您的 ASE 連接會保持作用中狀態，直到您關閉專案為止。 當您重新開啟專案時，如果您想要使用伺服器的作用中連接，就必須重新連接到 ASE。  
  
有關調適型伺服器的中繼資料不會自動更新。 相反地，如果您想要更新 Sybase Metadata Explorer 中的中繼資料，您必須手動更新中繼資料，如本主題稍後的「重新整理 Sybase ASE 中繼資料」一節中所述。  
  
## <a name="required-ase-permissions"></a>必要的 ASE 許可權

用來連接到 ASE 的帳戶必須至少具有 master 資料庫的**公用**存取權，以及要遷移至或 SQL Azure 的任何源資料庫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 此外，若要選取要遷移之資料表的許可權，使用者必須具有下列系統資料表的 SELECT 許可權：  
  
- [source_db] .dbo.sys物件  
- [source_db] .dbo.sys資料行  
- [source_db] .dbo.sys使用者  
- [source_db] .dbo.sys類型  
- [source_db] .dbo.sys條件約束  
- [source_db] .dbo.sys批註  
- [source_db] .dbo.sys索引  
- [source_db] .dbo.sys參考  
- master.dbo.sys資料庫  
  
## <a name="establishing-a-connection-to-ase"></a>建立 ASE 的連線

當您連接到調適型伺服器時，SSMA 會讀取資料庫伺服器上的資料庫中繼資料，然後將此中繼資料加入至專案檔。 當 SSMA 將物件轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Sql azure 語法，以及當它將資料移轉至或 Sql azure 時，會使用此中繼資料 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 您可以在 [Sybase 中繼資料瀏覽器] 窗格中流覽此中繼資料，並查看個別資料庫物件的屬性。  
  
> [!IMPORTANT]  
> 在您嘗試連接到資料庫伺服器之前，請確定資料庫伺服器正在執行，而且可以接受連接。  
  
**連接至 Sybase ASE**
  
1. 在 [檔案]**功能表上**，選取 **[連線到 Sybase]**。  
  
   如果您先前已連接到 Sybase，命令名稱會**重新連接到 sybase**。  
  
2. 在 [**提供者**] 方塊中，選取電腦上任何已安裝的提供者，以連線至 Sybase 伺服器。  
  
3. 在 [**模式]** 方塊中，選取 [**標準模式]** 或 [**先進模式]**。  
  
   使用 [標準模式] 來指定伺服器名稱、埠、使用者名稱和密碼。 使用 [advanced] 模式來提供連接字串。 此模式通常僅用於疑難排解或使用技術支援。  
  
4. 如果您選取 [**標準模式]**，請提供下列值：  
  
    1. 在 [**伺服器名稱**] 方塊中，輸入或選取資料庫伺服器的名稱或 IP 位址。  
    2. 如果資料庫伺服器未設定為接受預設通訊埠（5000）上的連接，請在 [**伺服器埠**] 方塊中輸入用於 Sybase 連接的通訊埠編號。  
    3. 在 [**使用者名稱**] 方塊中，輸入具有必要許可權的 Sybase 帳戶。  
    4. 在 [**密碼**] 方塊中，輸入指定之使用者名稱的密碼。  
  
5. 如果您選取 [**先進模式]**，請在 [**連接字串**] 方塊中提供連接字串。  
  
    不同連接字串的範例如下所示：  
  
    1. **Sybase OLE DB 提供者的連接字串：**  
  
        針對 Sybase ASE OLE DB 12.5，連接字串的範例如下所示：  
  
        `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
        針對 Sybase ASE OLE DB 15，連接字串的範例如下所示：  
  
        `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider= ASEOLEDB;Port=5000;`  
  
    2. **Sybase ODBC 提供者的連接字串：**  
  
       `Driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
    3. **Sybase ADO.NET 提供者的連接字串：**  
  
       `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
    如需詳細資訊，請參閱[連接到 Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)。  
  
## <a name="reconnecting-to-sybase-ase"></a>重新連接到 Sybase ASE

您的資料庫伺服器連接會保持作用中狀態，直到您關閉專案為止。 當您重新開啟專案時，如果您想要讓自我調整伺服器使用中的連接，就必須重新連接。 您可以離線工作，直到您想要更新中繼資料、將資料庫物件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure，以及遷移資料為止。  
  
## <a name="refreshing-sybase-ase-metadata"></a>重新整理 Sybase ASE 中繼資料

ASE 資料庫的相關中繼資料不會自動重新整理。 當您第一次連接到調適型伺服器時，或上次手動重新整理中繼資料時，Sybase Metadata Explorer 中的中繼資料就是中繼資料的快照集。 您可以手動更新單一資料庫、單一資料庫架構或所有資料庫的中繼資料。  
  
**重新整理中繼資料**
  
1. 請確定您已連接到調適型伺服器。  
  
2. 在 [Sybase Metadata Explorer] 中，選取您要更新之資料庫或資料庫架構旁的核取方塊。  
  
3. 以滑鼠右鍵按一下 [資料庫] 或個別資料庫或資料庫架構，然後選取 [**從資料庫**重新整理]。  
  
4. 如果系統要求您檢查目前的物件，請按一下 **[是]**。  
  
## <a name="next-step"></a>後續步驟  
  
- 遷移程式的下一個步驟是連接到[SQL Server](connecting-to-sql-server-sybasetosql.md)  /  [連接到 SQL Azure 實例](connecting-to-azure-sql-db-sybasetosql.md)的實例。  
  
## <a name="see-also"></a>另請參閱

[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
