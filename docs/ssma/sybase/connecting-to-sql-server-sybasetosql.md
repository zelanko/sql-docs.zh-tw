---
title: 連接到 SQL Server (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Connecting to SQL Server
ms.assetid: dd368a1a-45b0-40e9-b4d3-5cdb48c26606
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: aa44650e993ab23458daeaf454e2650a005b2461
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "40393798"
---
# <a name="connecting-to-sql-server-sybasetosql"></a>連線到 SQL Server (SybaseToSQL)
若要將 Sybase Adaptive Server Enterprise (ASE) 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您必須連接到任何目標執行個體的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 SSMA 連線時，取得執行個體中的所有資料庫的相關中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，並顯示資料庫中繼資料中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料總管。 SSMA 會將哪一個執行個體的相關資訊儲存[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您要連線，但不會儲存密碼。  
  
連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會保持作用中，直到您關閉專案為止。 當您重新開啟專案時，您必須重新連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果您想使用中的連接到伺服器。 您可以離線之前載入至資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]並移轉資料。  
  
執行個體相關的中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]並不會自動同步處理。 相反地，如果您想要更新的中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料總管 中，您必須手動更新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料，如中所述"Synchronizing[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料 」 在本主題稍後的章節。  
  
## <a name="required-sql-server-permissions"></a>所需的 SQL Server 權限  
用來連接到帳戶[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]需要不同的權限，根據該帳戶所執行的動作。  
  
-   要轉換至 ASE 物件[!INCLUDE[tsql](../../includes/tsql-md.md)]語法，來更新中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，或是要儲存指令碼轉換的語法，帳戶必須具備登入的執行個體的權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   資料庫物件載入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，最小權限需求是中的成員資格**db_owner**之目標資料庫內的資料庫角色。  
  
-   若要將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，帳戶應該是隸屬**sysadmin**伺服器角色。 如此才能執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式的資料移轉的套件。  
  
-   若要執行的程式碼所產生的 SSMA，帳戶必須具有**Execute**中的所有使用者定義函數的權限**ssma_syb**的結構描述**sysdb**資料庫。 這些函式提供 ASE 系統函式，對等的功能，並由已轉換的物件。  
  
如果帳戶是用來連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若要執行所有移轉工作，該帳戶必須是成員**sysadmin**伺服器角色。  
  
## <a name="establishing-a-sql-server-connection"></a>建立 SQL Server 連接  
轉換至 ASE 資料庫物件之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]語法中，您必須建立的執行個體的連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您要移轉的 ASE 資料庫。  
  
當您定義的連接屬性時，您也可以指定其中將移轉物件和資料的資料庫。 連線到之後，您可以自訂此 ASE 結構描述層級的對應[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱 <<c0> [ 對應 Sybase ASE 結構描述 SQL Server 結構描述&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)。</c0>  
  
> [!IMPORTANT]  
> 您嘗試連接到之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請確定執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在執行，而且可以接受連線。  
  
**若要連接到 SQL Server**  
  
1.  在 **檔案**功能表上，選取**連接到 SQL Server**。  
  
    如果您先前連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，命令名稱會是**重新連接到 SQL Server**。  
  
2.  在 [連線] 對話方塊中，輸入或選取的執行個體名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
    -   如果您要連接到本機電腦上的預設執行個體，您可以輸入**localhost**或句點 (**。**)。  
  
    -   如果您要連接到另一部電腦上的預設執行個體，請輸入電腦的名稱。  
  
    -   如果您要連接到另一部電腦上的具名執行個體，請輸入電腦名稱，後面接著反斜線，然後按一下 執行個體名稱，例如 MyServer\MyInstance。  
  
3.  如果您的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]設定為在非預設連接埠上接受連線中，輸入用於連接埠號碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的連線**伺服器連接埠** 方塊中。 預設執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，預設連接埠號碼為 1433年。 具名執行個體，SSMA 會嘗試取得連接埠號碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]瀏覽器服務。  
  
4.  在 **資料庫**方塊中，輸入目標資料庫的名稱。  
  
    此選項時，無法提供重新連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
5.  在 **驗證**方塊中，選取要用於連線的驗證類型。 若要使用目前的 Windows 帳戶，請選取**Windows 驗證**。 若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入，選取**SQL Server 驗證**]，然後提供 [登入名稱和密碼。  
  
6.  安全的連線，會新增兩個控制項，**加密連接**並**TrustServerCertificate**核取方塊。 只有當**加密連接**會檢查**TrustServerCertificate**核取方塊會顯示。 當**加密連接**核取 (true) 及**TrustServerCertificate**未核取 (false)，它將會驗證 SQL Server SSL 憑證。 驗證伺服器憑證是 SSL 交握的一部分，而且這麼做可以確保伺服器是所要連接的正確伺服器。 若要確保此行為，以及伺服器端上的用戶端必須安裝憑證。  
  
7.  按一下 **[連接]**。  
  
**較高的版本相容性**  
  
-   您將能夠連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008年及[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年並[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年並[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 建立移轉專案時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005年。  
  
-   您將能夠連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年並[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年並[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 建立移轉專案時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008年但不是能也就是連線到較低版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   您可以只連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年並[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時建立的專案是 SQL Server 2012 的 2016年。  
  
-   較高的版本相容性不是有效的 SQL Azure。  
  
||||||||
|-|-|-|-|-|-|-|
|**專案類型與目標伺服器版本**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (版本： 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (版本： 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />(Version:13.x)|SQL Azure|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|是|是|是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||是|是|是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014||||是|是|| 
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||是||  
|SQL Azure||||||是|  
  
> [!IMPORTANT]  
> 根據專案類型，但不是根據版本的資料庫物件的轉換會執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您已連線到。 中的案例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005年專案中，轉換會論及依照[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]即使您已連線到較高版本的 2005年[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016年)  
  
## <a name="reconnecting-to-sql-server"></a>重新連接到 SQL Server  
連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會保持作用中，直到您關閉專案為止。 當您重新開啟專案時，您必須重新連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果您想使用中的連接到伺服器。 您可以離線直到更新中繼資料，將資料庫物件載入到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，並移轉資料。  
  
若要重新連接的程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立連接的程序相同。  
  
## <a name="synchronizing-sql-server-metadata"></a>同步處理 SQL Server 中繼資料  
有關的中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫不會自動更新。 中的中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料總管 是中繼資料的快照集，當您第一次連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，或上一次您手動更新的中繼資料。 您可以手動更新所有資料庫，或任何單一資料庫或資料庫物件的中繼資料。  
  
**同步處理中繼資料**  
  
1.  請確定您連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
2.  在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料總管] 中，選取資料庫旁的核取方塊，或您想要更新的結構描述的資料庫。  
  
    例如，若要更新所有資料庫的中繼資料，選取旁**資料庫**。  
  
3.  以滑鼠右鍵按一下資料庫或個別資料庫或資料庫結構描述，然後按**同步處理資料庫**。  
  
## <a name="next-step"></a>下一個步驟  
移轉的下一個步驟取決於您的專案需求：  
  
-   如果您想要自訂 ASE 資料庫和結構描述之間的對應並[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫和結構描述，請參閱[Sybase ASE 結構描述對應到 SQL Server 結構描述&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)。  
  
-   如果您想要自訂專案的組態選項，請參閱[設定專案選項&#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)。  
  
-   如果您想自訂的來源和目標資料類型對應，請參閱[對應 Sybase ASE 和 SQL Server 資料類型&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)。  
  
-   如果您不需要進行這些，您可以將轉換成的 Sybase ASE 資料庫物件定義[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]物件定義。 如需詳細資訊，請參閱 <<c0> [ 轉換 Sybase ASE 資料庫物件&#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
