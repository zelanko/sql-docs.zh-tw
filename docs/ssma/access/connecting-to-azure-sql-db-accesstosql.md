---
title: 連線到 Azure SQL DB (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- instance of SQL Azure
- metadata, refreshing
- refreshing metadata
- SQL Azure
- SQL Azure, connecting
- SQL Azure, connecting to
- SQL Azure, reconnecting
- SQL Azure, synchronizing metadata
ms.assetid: 1ba0d113-dc05-4431-8689-e14a8821bafd
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8924ffbbbbbedccdc3bb99469c92667efb822a4c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63138918"
---
# <a name="connecting-to-azure-sql-db-accesstosql"></a>連線到 Azure SQL DB (AccessToSQL)
若要將 Access 資料庫移轉至 SQL Azure 中，您必須連接到 SQL Azure 的目標執行個體。 當您連線時，SSMA 取得 SQL Azure 執行個體中的所有資料庫的相關中繼資料，並在 SQL Azure 中繼資料總管 會顯示資料庫中繼資料。 SSMA 會儲存有關哪一個 SQL Azure 執行個體要連線，但不會儲存密碼的資訊。  
  
SQL Azure 的連線保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連接到 SQL Azure 是否作用中的連線到伺服器。 您的資料庫物件載入 SQL Azure，並移轉資料之前，您可以離線工作。  
  
SQL Azure 執行個體的相關中繼資料不會自動同步處理。 相反地，若要更新 SQL Azure 中繼資料總管 中的中繼資料，您必須手動更新 SQL Azure 中繼資料。 如需詳細資訊，請參閱本主題稍後的 「 同步處理 SQL Azure 中繼資料 」 一節。  
  
## <a name="required-sql-azure-permissions"></a>SQL Azure 的所需的權限  
用來連接到 SQL Azure 的帳戶需要不同的權限視帳戶執行的動作而定：  
  
-   要轉換到存取物件[!INCLUDE[tsql](../../includes/tsql-md.md)]語法，來更新中繼資料從 SQL Azure，或是儲存已轉換的語法，以編寫指令碼，該帳戶必須具有權限登入的 SQL Azure 執行個體。  
  
-   若要載入 SQL Azure 中的資料庫物件，最小權限需求是中的成員資格**db_owner**之目標資料庫內的資料庫角色。  
  
## <a name="establishing-a-sql-azure-connection"></a>建立 SQL Azure 的連線  
您將存取資料庫物件轉換成 SQL Azure 語法之前，您必須建立您要移轉的 Access 資料庫的 SQL Azure 的執行個體的連接。  
  
當您定義的連接屬性時，您也可以指定其中將移轉物件和資料的資料庫。 連線到 SQL Azure 之後，您可以自訂此存取結構描述層級的對應。 如需詳細資訊，請參閱[對應至 SQL Server 結構描述的 Access 資料庫](mapping-source-and-target-databases-accesstosql.md)  
  
> [!IMPORTANT]  
> 您嘗試連接到 SQL Azure，請確定之前的 SQL Azure 執行個體正在執行，而且可以接受連線。  
  
**若要連接到 SQL Azure**  
  
1.  在 **檔案**功能表上，選取**連接到 SQL Azure** （專案建立之後啟用此選項）。  
  
    如果您先前連線到 SQL Azure 時，命令名稱會是**重新連接到 SQL Azure**。  
  
2.  在 連線 對話方塊中，輸入或選取 SQL Azure 的伺服器名稱。  
  
3.  輸入中，選取或**瀏覽**資料庫名稱。  
  
4.  輸入或選取**UserName**。  
  
5.  請輸入**密碼**。  
  
6.  SSMA 會建議加密的連接到 SQL Azure。  
  
7.  按一下 **[連接]** 。  
  
> [!IMPORTANT]  
> SSMA for Access 不支援連接到**主要**中 SQL Azure 資料庫。  
  
如果沒有在 SQL Azure 帳戶中的資料庫，您可以建立第一次的資料庫使用**建立 Azure Database**選項會出現在上按一下**瀏覽** 按鈕。  
  
## <a name="synchronizing-sql-azure-metadata"></a>同步處理 SQL Azure 中繼資料  
SQL Azure 資料庫的相關中繼資料不會自動更新。 SQL Azure 中繼資料總管 中的中繼資料是快照集的中繼資料，當您第一次連接到 SQL Azure，或上一次，您以手動方式更新中繼資料。 您可以手動更新所有資料庫，或任何單一資料庫或資料庫物件的中繼資料。  
  
**同步處理中繼資料**  
  
1.  請確定您已連線到 SQL Azure。  
  
2.  在 SQL Azure 中繼資料總管，選取您想要更新的資料庫結構描述的資料庫旁邊的核取方塊。  
  
    比方說，若要更新所有資料庫的中繼資料，請選取資料庫旁的方塊。  
  
3.  以滑鼠右鍵按一下資料庫，或個別資料庫或資料庫結構描述，然後按**同步處理資料庫**。  
  
## <a name="refreshing-sql-azure-metadata"></a>重新整理 SQL Azure 中繼資料  
如果您連接之後，就會變更 SQL Azure 結構描述，您可以重新整理從伺服器的中繼資料。  
  
**若要重新整理 SQL Azure 中繼資料**  
  
-   在 SQL Azure 中繼資料總管，以滑鼠右鍵按一下**資料庫**，然後選取**從資料庫重新整理**。  
  
## <a name="reconnecting-to-sql-azure"></a>重新連接到 SQL Azure  
SQL Azure 的連線保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連接到 SQL Azure 是否作用中的連線到伺服器。 您的資料庫物件載入 SQL Azure，並移轉資料之前，您可以離線工作。  
  
重新連接到 SQL Azure 的程序是建立連接的程序相同。  
  
## <a name="next-step"></a>下一個步驟  
移轉的下一個步驟取決於您的專案需求：  
  
-   若要自訂存取結構描述和 SQL Azure 資料庫和結構描述之間的對應，請參閱[對應至 SQL Server 結構描述的 Access 資料庫](mapping-source-and-target-databases-accesstosql.md)。  
  
-   若要自訂專案的組態選項，請參閱[設定專案選項](setting-conversion-and-migration-options-accesstosql.md)。  
  
-   若要自訂的來源和目標資料類型對應，請參閱[對應來源和目標資料型別](mapping-source-and-target-data-types-accesstosql.md)。  
  
-   如果您不需要執行任何這些工作，您可以存取資料庫物件定義轉換 SQL Azure 物件定義。 如需詳細資訊，請參閱[轉換 Access 資料庫](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
