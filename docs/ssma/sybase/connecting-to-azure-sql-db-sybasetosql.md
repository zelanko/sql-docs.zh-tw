---
title: 連線到 Azure SQL DB (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ac8b97e36338a280b6f78a0e6bb73eeab882655d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632096"
---
# <a name="connecting-to-azure-sql-db-sybasetosql"></a>連線到 Azure SQL DB (SybaseToSQL)
若要將 Sybase 資料庫移轉至 Azure SQL DB 中，您必須連接到 Azure SQL DB 的目標執行個體。 當您連線時，SSMA 取得 Azure SQL DB 執行個體中的所有資料庫的相關中繼資料，並會顯示在 Azure SQL DB 中繼資料總管 中的資料庫中繼資料。 SSMA 會儲存您要連線，但不會儲存密碼，Azure SQL DB 執行個體的資訊。  
  
您到 Azure SQL DB 的連線保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連線到 Azure SQL DB 如果您想使用中的連接到伺服器。 載入 Azure SQL DB 中的資料庫物件，並移轉資料之前，您可以離線工作。  
  
Azure SQL DB 執行個體的相關中繼資料不會自動同步處理。 相反地，若要更新 Azure SQL DB 中繼資料總管 中的中繼資料，您必須手動更新 Azure SQL DB 中繼資料。 如需詳細資訊，請參閱本主題稍後的 「 同步處理 Azure SQL DB 中繼資料 」 一節。  
  
## <a name="required-azure-sql-db-permissions"></a>必要的 Azure SQL DB 權限  
用來連接到 Azure SQL DB 的帳戶需要不同的權限視帳戶執行的動作而定：  
  
1.  若要轉換 Sybase 物件[!INCLUDE[tsql](../../includes/tsql-md.md)]語法，來更新中繼資料從 Azure SQL DB，或將儲存已轉換的語法，以編寫指令碼，該帳戶必須具有登入 Azure SQL db 執行個體的權限。  
  
2.  若要載入 Azure SQL DB 中的資料庫物件，最小權限需求是中的成員資格**db_owner**之目標資料庫內的資料庫角色。  
  
## <a name="establishing-a-azure-sql-db-connection"></a>建立 Azure SQL DB 連接  
您將 Sybase 資料庫物件轉換成 Azure SQL DB 語法之前，您必須建立 Azure SQL db，您要移轉的 Sybase 資料庫執行個體的連接。  
  
當您定義的連接屬性時，您也可以指定其中將移轉物件和資料的資料庫。 連線到 Azure SQL DB 之後，您可以自訂這個對應 Sybase 結構描述層級。 如需詳細資訊，請參閱 <<c0> [ 對應 Sybase ASE 結構描述 SQL Server 結構描述&#40;SybaseToSQL&#41;</c0>](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
> [!WARNING]  
> 您嘗試連線到 Azure SQL DB，請確定之前的 Azure SQL DB 執行個體正在執行，而且可以接受連線。  
  
**若要連線到 Azure SQL DB**  
  
1.  在 **檔案**功能表上，選取**連線到 Azure SQL DB**（專案建立之後啟用此選項）。  
  
    如果您先前曾經連線到 Azure SQL DB，命令名稱會是**重新連接到 Azure SQL DB**  
  
2.  在 [連線] 對話方塊中，輸入或選取 Azure SQL DB 的伺服器名稱。  
  
3.  輸入中，選取或**瀏覽**資料庫名稱。  
  
4.  輸入或選取**UserName**。  
  
5.  請輸入**密碼**。  
  
6.  SSMA 會建議加密的連線到 Azure SQL DB。  
  
7.  按一下 **[連接]**。  
  
> [!IMPORTANT]  
> SSMA for Sybase 不支援連接到**主要**Azure SQL DB 中的資料庫。  
  
## <a name="synchronizing-azure-sql-db-metadata"></a>同步處理的 Azure SQL DB 中繼資料  
Azure SQL DB 資料庫的相關中繼資料不會自動更新。 Azure SQL DB 中繼資料總管 中的中繼資料是中繼資料的快照集，當您第一次連線到 Azure SQL DB 或以手動方式更新中繼資料的時間。 您可以手動更新所有資料庫，或任何單一資料庫或資料庫物件的中繼資料。  
  
**同步處理中繼資料**  
  
1.  請確定您已連線到 Azure SQL DB。  
  
2.  在 Azure SQL DB 中繼資料總管，選取您想要更新的資料庫結構描述的資料庫旁邊的核取方塊。  
  
    比方說，若要更新所有資料庫的中繼資料，請選取資料庫旁的方塊。  
  
3.  以滑鼠右鍵按一下資料庫，或個別資料庫或資料庫結構描述，然後按**同步處理資料庫**。  
  
## <a name="next-step"></a>下一個步驟  
移轉的下一個步驟取決於您的專案需求：  
  
-   若要自訂 Sybase 結構描述和 Azure SQL DB 資料庫和結構描述之間的對應，請參閱[Sybase ASE 結構描述對應到 SQL Server 結構描述&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
-   若要自訂專案的組態選項，請參閱[設定專案選項&#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)  
  
-   若要自訂的來源和目標資料類型對應，請參閱[對應 Sybase ASE 和 SQL Server 資料類型&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)  
  
-   如果您不需要執行任何這些工作，您可以將 Sybase 資料庫物件定義轉換到 Azure SQL DB 物件定義。 如需詳細資訊，請參閱 <<c0> [ 轉換 Sybase ASE 資料庫物件&#40;SybaseToSQL&#41;</c0>](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
