---
title: 連接到 SQL Server (MySQLToSQL) |Microsoft Docs
ms.prod: sql
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
- connecting to SQL Server 2008, SQL Server permission
- connecting to SQL Server 2008, synchronization
ms.assetid: 08233267-693e-46e6-9ca3-3a3dfd3d2be7
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 08744f04acbc5ad066be78b90f8880459ce74629
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "40396456"
---
# <a name="connecting-to-sql-server-mysqltosql"></a>連線到 SQL Server (MySQLToSQL)
若要將 MySQL 資料庫移轉至 SQL Server 中，您必須連接到 SQL Server 目標執行個體。 連線時，SSMA 取得 SQL Server 執行個體中的所有資料庫的相關中繼資料，並在 SQL Server 中繼資料總管 會顯示資料庫中繼資料。 SSMA 會儲存您要連線，但不會儲存密碼的 SQL Server 執行個體的資訊。  
  
SQL Server 的連接會保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連接到 SQL Server 是否作用中的連線到伺服器。 您的資料庫物件載入 SQL Server，並移轉資料之前，您可以離線工作。  
  
SQL Server 執行個體的相關中繼資料不會自動同步處理。 相反地，若要更新 SQL Server 中繼資料總管 中的中繼資料，您必須手動更新 SQL Server 中繼資料。 如需詳細資訊，請參閱本主題稍後的 「 同步處理 SQL Server 中繼資料 」 一節。  
  
## <a name="required-sql-server-permissions"></a>所需的 SQL Server 權限  
用來連接到 SQL Server 的帳戶需要不同的權限視帳戶執行的動作而定：  
  
-   若要將 MySQL 物件[!INCLUDE[tsql](../../includes/tsql-md.md)]語法，來更新中繼資料從 SQL Server，或是儲存已轉換的語法，以編寫指令碼，該帳戶必須擁有登入的 SQL Server 執行個體的權限。  
  
-   若要載入 SQL Server 資料庫物件，最小權限需求是中的成員資格**db_owner**之目標資料庫內的資料庫角色。  
  
## <a name="establishing-a-sql-server-connection"></a>建立 SQL Server 連接  
您將 MySQL 資料庫物件轉換成 SQL Server 語法之前，您必須建立您要移轉的 MySQL 資料庫的 SQL Server 執行個體的連接。  
  
當您定義的連接屬性時，您也可以指定其中將移轉物件和資料的資料庫。 連線到 SQL Server 之後，您可以自訂這個 MySQL 結構描述層級的對應。 如需詳細資訊，請參閱 <<c0> [ 對應至 SQL Server 結構描述的 MySQL 資料庫&#40;MySQLToSQL&#41;</c0>](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> 您嘗試連接到 SQL Server 之前，請確定 SQL Server 執行個體正在執行，而且可以接受連線。  
  
**若要連接到 SQL Server**  
  
1.  在 **檔案**功能表上，選取**連接到 SQL Server** （專案建立之後啟用此選項）。  
  
    如果您先前已連線到 SQL Server，命令名稱會是**重新連接到 SQL Server**。  
  
2.  在 [連線] 對話方塊中，輸入或選取的 SQL Server 執行個體的名稱。  
  
    -   如果您要連接到本機電腦上的預設執行個體，您可以輸入**localhost**或句點 (**。**)。  
  
    -   如果您要連接到另一部電腦上的預設執行個體，請輸入電腦的名稱。  
  
    -   如果您要連接到另一部電腦上的具名執行個體，請輸入電腦名稱，後面接著反斜線，然後按一下 執行個體名稱，例如 MyServer\MyInstance。  
  
3.  如果您的 SQL Server 執行個體設定為在非預設連接埠上接受連線，請輸入用於中的 SQL Server 連線的連接埠號碼**伺服器的連接埠** 方塊中。 SQL Server 預設執行個體，預設連接埠號碼為 1433年。 具名執行個體，SSMA 會嘗試從 SQL Server Browser 服務取得的連接埠號碼。  
  
4.  在 **驗證**方塊中，選取要用於連線的驗證類型。 若要使用目前的 Windows 帳戶，請選取**Windows 驗證**。 若要使用的 SQL Server 登入，選取 [SQL Server 驗證]，然後提供的登入名稱和密碼。  
  
5.  安全的連線，會新增兩個控制項，**加密連接**並**TrustServerCertificate**核取方塊。 只有當**加密連接**會檢查**TrustServerCertificate**核取方塊會顯示。 當**加密連接**核取 (true) 及**TrustServerCertificate**未核取 (false)，它將會驗證 SQL Server SSL 憑證。 驗證伺服器憑證是 SSL 交握的一部分，而且這麼做可以確保伺服器是所要連接的正確伺服器。 若要確保此行為，以及伺服器端上的用戶端必須安裝憑證。  
  
6.  按一下 [連線]。  
  
**較高的版本相容性**  
  
它允許連線/重新連線到更高版本的 SQL Server。  
  
1.  您將能夠連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 建立的專案時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005年。  
  
2.  您將能夠連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 建立的專案時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008年，但是不能也就是連線到較低版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
3.  您將能夠連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 建立的專案時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年。  
  
4.  您可以只連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年或是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 建立的專案時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年。  
  
5.  較高的版本相容性的 「 SQL Azure"無效。  
  
||||||||  
|-|-|-|-|-|-|-|  
|**專案類型與目標伺服器版本**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (版本： 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (版本： 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012<br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014<br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016<br />(Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|是|是|是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||是|是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016|||||是||  
|SQL Azure||||||是|  
  
> [!IMPORTANT]  
> 根據專案類型，但不是根據版本的資料庫物件的轉換會執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連線到。 中的案例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005年專案中，轉換會論及依照[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]即使您已連線到較高版本的 2005年[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016)。  
  
## <a name="synchronizing-sql-server-metadata"></a>同步處理 SQL Server 中繼資料  
SQL Server 資料庫的相關中繼資料不會自動更新。 SQL Server 中繼資料總管 中的中繼資料是快照集的中繼資料，當您第一次連接到 SQL Server，或上一次，您以手動方式更新中繼資料。 您可以手動更新所有資料庫，或任何單一資料庫或資料庫物件的中繼資料。  
  
**同步處理中繼資料**  
  
1.  請確定您已連線到 SQL Server。  
  
2.  在 SQL Server 中繼資料總管，選取您想要更新的資料庫結構描述的資料庫旁邊的核取方塊。  
  
    比方說，若要更新所有資料庫的中繼資料，請選取資料庫旁的方塊。  
  
3.  以滑鼠右鍵按一下資料庫，或個別資料庫或資料庫結構描述，然後按**同步處理資料庫**。  
  
## <a name="next-step"></a>下一個步驟  
移轉的下一個步驟取決於您的專案需求：  
  
-   若要自訂 MySQL 結構描述和 SQL Server 資料庫和結構描述之間的對應，請參閱[對應至 SQL Server 結構描述的 MySQL 資料庫&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   若要自訂專案的組態選項，請參閱[設定專案選項&#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   若要自訂的來源和目標資料類型對應，請參閱[對應 MySQL 和 SQL Server 資料類型&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   如果您不需要執行任何這些工作，您將轉換的 MySQL 資料庫物件定義 SQL Server 物件定義。 如需詳細資訊，請參閱 <<c0> [ 轉換 MySQL 資料庫&#40;MySQLToSQL&#41;</c0>](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[移轉 MySQL 資料庫到 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
