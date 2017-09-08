---
title: "連接到 Azure SQL DB (SybaseToSQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 217492904d3d21818fed28222dcc6acaf193c92b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="connecting-to-azure-sql-db-sybasetosql"></a>連接到 Azure SQL DB (SybaseToSQL)
若要將 Sybase 資料庫移轉至 Azure SQL DB 中，您必須連接到 Azure SQL DB 的目標執行個體。 連線時，SSMA 取得 Azure SQL 資料庫執行個體中的所有資料庫的相關中繼資料，並在 Azure SQL DB 中繼資料總管 會顯示資料庫中繼資料。 SSMA 會儲存您連線到，但不會儲存密碼，Azure SQL 資料庫執行個體的資訊。  
  
Azure SQL DB 的連接會保持作用中直到您關閉專案。 當您重新開啟專案時，您必須重新連接到 Azure SQL DB 如果您想要的使用中連接到伺服器。 您載入 Azure SQL DB 中的資料庫物件，並移轉資料之前，您可以離線工作。  
  
Azure SQL 資料庫執行個體的相關中繼資料不會自動同步處理。 相反地，若要更新 Azure SQL DB 中繼資料總管 中的中繼資料，您必須手動更新 Azure SQL DB 中繼資料。 如需詳細資訊，請參閱本主題稍後的 「 同步處理 Azure SQL DB 中繼資料 」 一節。  
  
## <a name="required-azure-sql-db-permissions"></a>必要的 Azure SQL DB 權限  
用來連接到 Azure SQL DB 的帳戶需要不同的權限視帳戶執行的動作而定：  
  
1.  要轉換至 Sybase 物件[!INCLUDE[tsql](../../includes/tsql_md.md)]語法，來更新中繼資料從 Azure SQL DB、 或儲存已轉換的語法編寫的指令碼，帳戶必須具有執行個體的 Azure SQL DB 登入權限。  
  
2.  若要載入 Azure SQL DB 中的資料庫物件，最小權限需求是中的成員資格**db_owner**之目標資料庫內的資料庫角色。  
  
## <a name="establishing-a-azure-sql-db-connection"></a>建立 Azure SQL DB 連接  
您將 Sybase 資料庫物件轉換成 Azure SQL DB 語法之前，您必須建立 Azure SQL DB 您要移轉的 Sybase 資料庫的執行個體的連接。  
  
當您定義的連接屬性時，您也可以指定其中將移轉物件和資料的資料庫。 連接到 Azure SQL DB 之後，您可以自訂這個對應 Sybase 結構描述層級。 如需詳細資訊，請參閱[對應 Sybase ASE 結構描述，以 SQL Server 結構描述 &#40;SybaseToSQL &#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
> [!WARNING]  
> 您嘗試連接到 Azure SQL DB 之前，請確定 Azure SQL DB 的執行個體正在執行，以及可接受連接。  
  
**若要連接到 Azure SQL DB**  
  
1.  在**檔案**功能表上，選取**連接到 Azure SQL DB**（為專案建立之後啟用此選項）。  
  
    如果您之前已連線到 Azure SQL DB，命令名稱將**重新連接到 Azure SQL DB**  
  
2.  在 [連線] 對話方塊中，輸入或選取的 Azure SQL DB 伺服器名稱。  
  
3.  輸入中，選取或**瀏覽**資料庫名稱。  
  
4.  輸入或選取**UserName**。  
  
5.  輸入**密碼**。  
  
6.  SSMA 會建議加密的連接到 Azure SQL DB。  
  
7.  按一下 **[連接]**。  
  
> [!IMPORTANT]  
> SSMA for Sybase 不支援連接**主要**Azure SQL DB 中的資料庫。  
  
## <a name="synchronizing-azure-sql-db-metadata"></a>同步處理 Azure SQL DB 中繼資料  
Azure SQL DB 資料庫的相關中繼資料不會自動更新。 Azure SQL DB 中繼資料總管 中的中繼資料是中繼資料的快照集，當您第一次連線到 Azure SQL DB、 或上次手動更新中繼資料。 您可以手動更新所有資料庫，或任何單一資料庫或資料庫物件的中繼資料。  
  
**同步處理中繼資料**  
  
1.  請確定您已連線到 Azure SQL DB。  
  
2.  在 Azure SQL DB 中繼資料總管，選取您想要更新的資料庫結構描述的資料庫旁邊的核取方塊。  
  
    例如，若要更新所有資料庫的中繼資料，選取資料庫旁的方塊。  
  
3.  資料庫或個別的資料庫或資料庫結構描述，以滑鼠右鍵按一下，然後選取**同步處理資料庫**。  
  
## <a name="next-step"></a>下一個步驟  
移轉的下一個步驟取決於您專案的需求：  
  
-   若要自訂 Sybase 結構描述和 Azure SQL DB 資料庫和結構描述之間的對應，請參閱[對應至 SQL Server 結構描述 &#40; Sybase ASE 結構描述SybaseToSQL &#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
-   若要自訂專案的組態選項，請參閱[設定專案選項 &#40;SybaseToSQL &#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)  
  
-   若要自訂的來源和目標資料類型對應，請參閱[對應 Sybase ASE 和 SQL Server 資料類型 &#40;SybaseToSQL &#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)  
  
-   如果您不需要執行任何這些工作，您可以在 Azure SQL DB 物件定義轉換 Sybase 資料庫物件定義。 如需詳細資訊，請參閱[轉換 Sybase ASE 資料庫物件 &#40;SybaseToSQL &#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[Sybase ASE 將資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

