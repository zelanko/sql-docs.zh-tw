---
title: 連接到 Sybase ASE (SybaseToSQL) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Connecting to Sybase ASE
ms.assetid: a45a2330-9175-4c9e-af38-ef920e350614
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: fc01dc51a4c3b50e77a719d9b3bab08def84f879
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="connecting-to-sybase-ase-sybasetosql"></a>連接到 Sybase ASE (SybaseToSQL)
若要將 Sybase Adaptive Server Enterprise (ASE) 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，您必須連接到自動調整的伺服器，其中包含您想要移轉的資料庫。 當您連線時，SSMA 會取得自動調整的伺服器上的所有資料庫的相關中繼資料和 Sybase 中繼資料總管 窗格中顯示資料庫中繼資料。 SSMA 會儲存在資料庫伺服器的相關資訊，但不會儲存密碼。  
  
ASE 的連接會保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連接到 ASE 如果您想要的使用中連接到伺服器。  
  
自動調整的伺服器相關的中繼資料不會自動更新。 相反地，如果您想要更新 Sybase 中繼資料總管 中的中繼資料，您必須手動更新中繼資料，如本主題稍後的 「 重新整理 Sybase ASE 中繼資料 」 一節所述。  
  
## <a name="required-ase-permissions"></a>需要的 ASE 權限  
用來連接到 ASE 帳戶至少必須有**公用**存取 master 資料庫與來源資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 此外，若要選取要移轉的資料表上的權限，使用者必須有 SELECT 權限上的下列系統資料表：  
  
-   [source_db].dbo.sysobjects  
  
-   [source_db].dbo.syscolumns  
  
-   [source_db].dbo.sysusers  
  
-   [source_db].dbo.systypes  
  
-   [source_db].dbo.sysconstraints  
  
-   [source_db].dbo.syscomments  
  
-   [source_db].dbo.sysindexes  
  
-   [source_db].dbo.sysreferences  
  
-   master.dbo.sysdatabases  
  
## <a name="establishing-a-connection-to-ase"></a>建立連線至 ASE  
當您連接到自動調整的伺服器時，SSMA 讀取資料庫中繼資料，在資料庫伺服器上的，然後將此中繼資料加入至專案檔。 此中繼資料時，會使用 SSMA 會將轉換的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的語法，以及當它能將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 您可以瀏覽此 Sybase 中繼資料總管 窗格中的中繼資料，並檢視個別資料庫物件的屬性。  
  
> [!IMPORTANT]  
> 您嘗試連接到資料庫伺服器之前，請確定資料庫伺服器正在執行，且可接受連接。  
  
**若要連接到 Sybase ASE**  
  
1.  在**檔案**功能表上，選取**連接到 Sybase**。  
  
    如果您先前連接到 Sybase，命令名稱將**重新連接到 Sybase**。  
  
2.  在**提供者**方塊中，選取任何連接到 Sybase 伺服器電腦上已安裝提供者。  
  
3.  在**模式**方塊中，選取 **標準模式**或**進階的模式**。  
  
    使用標準模式來指定伺服器名稱、 連接埠、 使用者名稱和密碼。 使用進階的模式來提供連接字串。 此模式通常是只用於疑難排解，或使用 技術支援人員。  
  
4.  如果您選取**標準模式**，提供下列值：  
  
    1.  在**伺服器名稱**方塊中，輸入或選取的名稱或資料庫伺服器的 IP 位址。  
  
    2.  如果資料庫伺服器未設定為接受連接的預設通訊埠 (5000)，請輸入用於 Sybase 連線中的連接埠號碼**伺服器連接埠**方塊。  
  
    3.  在**使用者名**方塊中，輸入 Sybase 帳戶具有必要的權限。  
  
    4.  在**密碼**方塊中，指定的使用者名稱輸入的密碼。  
  
5.  如果您選取**進階的模式**，提供連接字串中的**連接字串**方塊。  
  
    不同的連接字串的範例如下所示：  
  
    1.  **Sybase OLE DB 提供者的連接字串：**  
  
        Sybase ASE OLE DB 12.5，連接字串範例如下：  
  
        `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
        適用於 Sybase ASE OLE DB 15，連接字串範例如下所示：  
  
        `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider= ASEOLEDB;Port=5000;`  
  
    2.  **Sybase ODBC 提供者的連接字串：**  
  
        `Driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
    3.  **Sybase 的 ADO.NET 提供者的連接字串：**  
  
        `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
    如需詳細資訊，請參閱[連接到 Sybase &#40;SybaseToSQL &#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md).  
  
## <a name="reconnecting-to-sybase-ase"></a>重新連接到 Sybase ASE  
資料庫伺服器的連接會保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連接，如果您想要調整的伺服器的作用中連接。 您可以離線直到您想要更新中繼資料，資料庫物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 移轉資料。  
  
## <a name="refreshing-sybase-ase-metadata"></a>重新整理 Sybase ASE 中繼資料  
ASE 資料庫的相關中繼資料不會自動重新整理。 Sybase 中繼資料總管 中的中繼資料是中繼資料的快照集，當您第一次連接到自動調整的伺服器或您手動重新整理中繼資料的最後一次。 您可以手動更新單一資料庫中，單一資料庫結構描述或所有資料庫的中繼資料。  
  
**若要重新整理中繼資料**  
  
1.  請確定您已連線到自動調整的伺服器。  
  
2.  在 Sybase 中繼資料總管，選取您想要更新的資料庫結構描述的資料庫旁邊的核取方塊。  
  
3.  資料庫或個別的資料庫或資料庫結構描述，以滑鼠右鍵按一下，然後選取**從資料庫重新整理**。  
  
4.  如果要求您檢查目前的物件時，按一下**是**。  
  
## <a name="next-step"></a>下一個步驟  
  
-   移轉程序的下一個步驟是[連接到 SQL Server 執行個體](http://msdn.microsoft.com/en-us/dd368a1a-45b0-40e9-b4d3-5cdb48c26606) / [連接到 SQL Azure 的執行個體](http://msdn.microsoft.com/en-us/9e77e4b0-40c0-455c-8431-ca5d43849aa7)  
  
## <a name="see-also"></a>請參閱  
[Sybase ASE 將資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
