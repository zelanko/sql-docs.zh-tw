---
title: 連線到 Sybase ASE (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to Sybase ASE
ms.assetid: a45a2330-9175-4c9e-af38-ef920e350614
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d9c76a33a650284fde21b28af3a61b197829ef98
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298536"
---
# <a name="connecting-to-sybase-ase-sybasetosql"></a>連線到 Sybase ASE (SybaseToSQL)
若要將 Sybase Adaptive Server Enterprise (ASE) 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，您必須連接到包含您想要移轉的資料庫的自適性伺服器。 當您連線時，SSMA 取得自動調整的伺服器上的所有資料庫的相關中繼資料和 Sybase 中繼資料總管 窗格中顯示資料庫中繼資料。 SSMA 會儲存在資料庫伺服器的相關資訊，但不會儲存密碼。  
  
ASE 的連接會保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連接到 ASE 如果您想使用中的連接到伺服器。  
  
自適性伺服器相關的中繼資料不會自動更新。 相反地，如果您想要更新 Sybase 中繼資料總管 中的中繼資料，您必須手動更新中繼資料，如本主題稍後的 「 重新整理 Sybase ASE 中繼資料 」 一節中所述。  
  
## <a name="required-ase-permissions"></a>ASE 所需的權限  
用來連接到 ASE 的帳戶至少必須有**公開金鑰**存取 master 資料庫與來源資料庫移轉到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 此外，若要選取要移轉的資料表上的權限，使用者必須擁有 SELECT 權限在下列系統資料表上：  
  
-   [source_db].dbo.sysobjects  
  
-   [source_db].dbo.syscolumns  
  
-   [source_db].dbo.sysusers  
  
-   [source_db].dbo.systypes  
  
-   [source_db].dbo.sysconstraints  
  
-   [source_db].dbo.syscomments  
  
-   [source_db].dbo.sysindexes  
  
-   [source_db].dbo.sysreferences  
  
-   master.dbo.sysdatabases  
  
## <a name="establishing-a-connection-to-ase"></a>建立 ASE 的連接  
當您連接到自動調整的伺服器時，SSMA 讀取資料庫中繼資料，在資料庫伺服器上的，然後將此中繼資料新增至專案檔。 將轉換的物件時，使用此中繼資料的 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 的語法，以及當它將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 您可以瀏覽這個 Sybase 中繼資料總管 窗格中的中繼資料，然後檢閱個別的資料庫物件的屬性。  
  
> [!IMPORTANT]  
> 您嘗試連接到資料庫伺服器之前，請確定資料庫伺服器正在執行，而且可以接受連線。  
  
**若要連接到 Sybase ASE**  
  
1.  在 **檔案**功能表上，選取**連接到 Sybase**。  
  
    如果您先前連線到 Sybase，命令名稱會是**重新連接到 Sybase**。  
  
2.  在 **提供者**方塊中，選取任何連接到 Sybase 伺服器的電腦上已安裝提供者。  
  
3.  在 **模式**方塊中，選取**標準模式**或是**進階的模式**。  
  
    您可以使用標準模式來指定伺服器名稱、 連接埠、 使用者名稱和密碼。 使用進階的模式來提供連接字串。 此模式通常是只用於疑難排解，或與技術支援人員合作。  
  
4.  如果您選取**標準模式**，提供下列值：  
  
    1.  在 **伺服器名稱**方塊中，輸入或選取的資料庫伺服器的 IP 位址的名稱。  
  
    2.  如果資料庫伺服器未設定為接受連接的預設連接埠 (5000) 中，輸入的 Sybase 連線中使用的連接埠號碼**伺服器的連接埠** 方塊中。  
  
    3.  在 **使用者名**方塊中，輸入 Sybase 帳戶具有必要的權限。  
  
    4.  在 **密碼**方塊中，指定的使用者名稱輸入的密碼。  
  
5.  如果您選取**進階的模式**，以提供連接字串**連接字串** 方塊中。  
  
    不同的連接字串的範例如下所示：  
  
    1.  **Sybase OLE DB 提供者的連接字串：**  
  
        Sybase ASE OLE DB 12.5，為連接字串範例如下所示：  
  
        `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
        適用於 Sybase ASE OLE DB 15，連接字串範例如下所示：  
  
        `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider= ASEOLEDB;Port=5000;`  
  
    2.  **Sybase ODBC 提供者的連接字串：**  
  
        `Driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
    3.  **Sybase ADO.NET 提供者的連接字串：**  
  
        `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
    如需詳細資訊，請參閱 <<c0> [ 連接到 Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)。</c0>  
  
## <a name="reconnecting-to-sybase-ase"></a>重新連接到 Sybase ASE  
資料庫伺服器的連接會保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連線，如果您想要自動調整的伺服器的作用中連接。 您可以離線直到您想要更新中繼資料，資料庫物件載入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，並移轉資料。  
  
## <a name="refreshing-sybase-ase-metadata"></a>重新整理 Sybase ASE 中繼資料  
ASE 資料庫的相關中繼資料不會自動重新整理。 Sybase 中繼資料總管 中的中繼資料是中繼資料的快照集，當您第一次連線到彈性的伺服器或您手動重新整理中繼資料的最後一次。 您可以手動更新單一資料庫、 單一資料庫結構描述，或所有資料庫的中繼資料。  
  
**若要重新整理中繼資料**  
  
1.  請確定您已連線到自動調整的伺服器。  
  
2.  在 Sybase 中繼資料總管 中，選取您想要更新的資料庫結構描述的資料庫旁邊的核取方塊。  
  
3.  以滑鼠右鍵按一下資料庫或個別資料庫或資料庫結構描述，然後按**從資料庫重新整理**。  
  
4.  如果系統要求您檢查目前的物件時，按一下**是**。  
  
## <a name="next-step"></a>下一個步驟  
  
-   移轉程序的下一個步驟是[連接到 SQL Server 的執行個體](connecting-to-sql-server-sybasetosql.md) / [連接到 SQL Azure 的執行個體](connecting-to-azure-sql-db-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
