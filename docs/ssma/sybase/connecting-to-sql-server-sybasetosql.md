---
title: 連接到 SQL Server （SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Server
ms.assetid: dd368a1a-45b0-40e9-b4d3-5cdb48c26606
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 4f40fd6fa88b001eaa222789d6be35b83f9bf90a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948540"
---
# <a name="connecting-to-sql-server-sybasetosql"></a>連線到 SQL Server (SybaseToSQL)
若要將 Sybase 自我調整伺服器企業（ASE） [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫移轉至，您必須連接到的任何目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例。 當您連接時，SSMA 會取得實例中所有資料庫的相關元[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料，並在 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料] Explorer 中顯示資料庫中繼資料。 SSMA 會儲存您所連接之[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例的相關資訊，但不會儲存密碼。  
  
您的連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會保持作用中狀態，直到您關閉專案為止。 當您重新開啟專案時，如果您想[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]要使用伺服器的作用中連接，就必須重新連接到。 在您將資料庫物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]並遷移資料之前，您可以離線工作。  
  
與實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]相關的中繼資料不會自動同步處理。 相反地，如果您想要更新中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Explorer 中的中繼資料，則必須[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]手動更新中繼資料，如本主題[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]稍後的「同步處理中繼資料」一節中所述。  
  
## <a name="required-sql-server-permissions"></a>必要的 SQL Server 許可權  
用來連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的帳戶需要不同的許可權，視該帳戶所執行的動作而定。  
  
-   若要將 ASE 物件[!INCLUDE[tsql](../../includes/tsql-md.md)]轉換成語法、更新中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的中繼資料，或將已轉換的語法儲存至腳本，此帳戶必須具有登入實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的許可權。  
  
-   若要將資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]載入，最低許可權需求是目標資料庫中**db_owner**資料庫角色的成員資格。  
  
-   若要將資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]遷移至，帳戶必須是**系統管理員（sysadmin** ）伺服器角色的成員。 這是執行代理程式資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]遷移封裝的必要參數。  
  
-   若要執行 SSMA 所產生的程式碼，該帳戶必須擁有**sysdb**資料庫的**ssma_syb**架構中所有使用者定義函數的**執行**許可權。 這些函式會提供 ASE 系統函式的對等功能，並由已轉換的物件使用。  
  
如果用來連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的帳戶是執行所有的遷移工作，則該帳戶必須是**系統管理員（sysadmin** ）伺服器角色的成員。  
  
## <a name="establishing-a-sql-server-connection"></a>建立 SQL Server 連接  
將 ASE 資料庫物件轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]語法之前，您必須先建立要遷移 ASE 資料庫或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫之實例的連接。  
  
當您定義連接屬性時，也會指定要遷移物件和資料的資料庫。 連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之後，您可以在 ASE 架構層級自訂此對應。 如需詳細資訊，請參閱[將 SYBASE ASE 架構對應至 SQL Server 架構 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)。  
  
> [!IMPORTANT]  
> 在您嘗試連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，請確定的實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在執行，而且可以接受連接。  
  
**若要連接到 SQL Server**  
  
1.  在 [檔案]**功能表上**，選取 **[連線至 SQL Server]**。  
  
    如果您先前已連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到，命令名稱會**重新連接到 SQL Server**。  
  
2.  在 [連接] 對話方塊中，輸入或選取實例的名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
    -   如果您要連接到本機電腦上的預設實例，您可以輸入**localhost**或句點（**.**）。  
  
    -   如果您要連接到另一部電腦上的預設實例，請輸入電腦的名稱。  
  
    -   如果您要連接到另一部電腦上的已命名實例，請輸入電腦名稱稱，後面接著反斜線，然後是實例名稱，例如 MyServer\MyInstance。  
  
3.  如果您的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例設定為接受非預設通訊埠上的連接，請在 [**伺服器埠**] 方塊中輸入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用於連接的通訊埠編號。 預設實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的預設埠號碼為1433。 若為已命名的實例，SSMA 將會嘗試從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務取得埠號碼。  
  
4.  在 [**資料庫**] 方塊中，輸入目標資料庫的名稱。  
  
    重新連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，無法使用此選項。  
  
5.  在 [**驗證**] 方塊中，選取要用於連接的驗證類型。 若要使用目前的 Windows 帳戶，請選取 [ **Windows 驗證**]。 若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入，請選取 [ **SQL Server Authentication** ]，然後提供 [登入名稱] 和 [密碼]。  
  
6.  針對安全連線，會加入兩個控制項： [**加密連接**] 和 [ **TrustServerCertificate** ] 核取方塊。 只有在核取 [**加密連接**] 時，才會顯示 [ **TrustServerCertificate** ] 核取方塊。 若已核取 [**加密**連線] （true），而且未選取 [ **TrustServerCertificate** （false）]，則會驗證 SQL Server SSL 憑證。 驗證伺服器憑證是 SSL 交握的一部分，而且這麼做可以確保伺服器是所要連接的正確伺服器。 若要確保這一點，憑證必須安裝在用戶端以及伺服器端。  
  
7.  按一下 [ **連接**]。  
  
**版本相容性較高**  
  
-   當建立的遷移專案[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [2005] 時，您將能夠連線至2008和2012，以及2014和2016。  
  
-   當建立的遷移專案[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 時，您將能夠連線到2012和2014及2016，但您將無法連接到較低版本，也就[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是2005。  
  
-   當建立的專案是 SQL Server 2012 時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]只能連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到2012和2014和2016。  
  
-   較高版本的相容性對 SQL Azure 而言無效。  
  
||||||||
|-|-|-|-|-|-|-|
|**專案類型與目標伺服器版本**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005<br /> （版本： 9. x）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008<br /> （版本： 10. x）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 <br />（版本： 11. x）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 <br />（版本： 12. x）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />（版本： 13. x）|SQL Azure|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005|是|是|是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008||是|是|是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012|||是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||是|是|| 
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||是||  
|SQL Azure||||||是|  
  
> [!IMPORTANT]
> 資料庫物件的轉換是根據專案類型執行，而不是依據您所連接之的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若是2005專案，即使您連接至較高版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或2012或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016），還是會以每個2005執行轉換。  
  
## <a name="reconnecting-to-sql-server"></a>重新連接到 SQL Server  
您的連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會保持作用中狀態，直到您關閉專案為止。 當您重新開啟專案時，如果您想[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]要使用伺服器的作用中連接，就必須重新連接到。 您可以在更新中繼資料、將資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]載入及遷移資料之前，離線工作。  
  
重新連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的程式與建立連線的過程相同。  
  
## <a name="synchronizing-sql-server-metadata"></a>同步處理 SQL Server 中繼資料  
資料庫的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]相關中繼資料不會自動更新。 中繼資料 Explorer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的中繼資料是當您第一次連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，或上次手動更新中繼資料時的中繼資料快照集。 您可以手動更新所有資料庫或任何單一資料庫或資料庫物件的中繼資料。  
  
**同步處理中繼資料**  
  
1.  請確定您已連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
2.  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [中繼資料瀏覽器] 中，選取您要更新之資料庫或資料庫架構旁的核取方塊。  
  
    例如，若要更新所有資料庫的中繼資料，請選取 [**資料庫**] 旁的方塊。  
  
3.  以滑鼠右鍵按一下 [資料庫] 或個別資料庫或資料庫架構，然後選取 [**與資料庫同步處理**]。  
  
## <a name="next-step"></a>後續步驟  
遷移的下一個步驟取決於您的專案需求：  
  
-   如果您想要自訂 ASE 資料庫與架構和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫和架構之間的對應，請參閱[將 Sybase ASE 架構對應至 SQL Server 架構 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)。  
  
-   如果您想要自訂專案的設定選項，請參閱[&#40;SybaseToSQL&#41;設定專案選項](../../ssma/sybase/setting-project-options-sybasetosql.md)。  
  
-   如果您想要自訂來源和目標資料類型的對應，請參閱將[SYBASE ASE 和 SQL Server 資料類型對應 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)。  
  
-   如果您不需要執行任何動作，您可以將 Sybase ASE 資料庫物件定義轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]物件定義。 如需詳細資訊，請參閱將[SYBASE ASE 資料庫物件轉換 &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
