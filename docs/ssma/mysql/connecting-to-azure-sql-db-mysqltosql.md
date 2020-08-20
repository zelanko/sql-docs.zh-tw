---
description: '連接至 Azure SQL Database (MySQLToSQL) '
title: 連接至 Azure SQL Database (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Azure, SQL Azure permissions
- Connecting to SQL Azure, synchronization
ms.assetid: d0b6f16a-1880-459d-a0c7-28b7ef15c56a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 0f02c136251a45e27267ca89292d6bb5b39ffc75
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454140"
---
# <a name="connecting-to-azure-sql-database-mysqltosql"></a>連接至 Azure SQL Database (MySQLToSQL) 
若要將 MySQL 資料庫遷移至 SQL Azure，您必須連接至 SQL Azure 的目標實例。 當您連接時，SSMA 會取得 SQL Azure 實例中所有資料庫的相關中繼資料，並在 SQL Azure 中繼資料瀏覽器中顯示資料庫中繼資料。 SSMA 會儲存您所連接之 SQL Azure 實例的資訊，但不會儲存密碼。  
  
您與 SQL Azure 的連線會保持作用中狀態，直到您關閉專案為止。 當您重新開啟專案時，如果您想要使用中的伺服器連線，則必須重新連接至 SQL Azure。 您可以離線工作，直到您將資料庫物件載入 SQL Azure 並遷移資料為止。  
  
關於 SQL Azure 實例的中繼資料不會自動同步處理。 相反地，若要更新 SQL Azure 中繼資料瀏覽器中的中繼資料，您必須手動更新 SQL Azure 中繼資料。 如需詳細資訊，請參閱本主題稍後的「同步處理 SQL Azure 中繼資料」一節。  
  
## <a name="required-sql-azure-permissions"></a>必要的 SQL Azure 許可權  
用來連接至 SQL Azure 的帳戶需要不同的許可權，視帳戶執行的動作而定：  
  
-   若要將 MySQL 物件轉換成 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法、更新 Sql azure 的中繼資料，或將轉換的語法儲存至腳本，此帳戶必須具有登入 Sql azure 實例的許可權。  
  
-   若要將資料庫物件載入 SQL Azure 中，最低許可權需求是目標資料庫中 **db_owner** 資料庫角色的成員資格。  
  
## <a name="establishing-a-sql-azure-connection"></a>建立 SQL Azure 連接  
將 MySQL 資料庫物件轉換成 SQL Azure 語法之前，您必須先建立與 SQL Azure 實例的連接，您想要將 MySQL 資料庫遷移至其中。  
  
當您定義連接屬性時，您也會指定要遷移物件和資料的資料庫。 您可以在連接到 SQL Azure 之後，在 MySQL 架構層級自訂此對應。 如需詳細資訊，請參閱 [將 MySQL 資料庫對應至 SQL Server 架構 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> 在您嘗試連線到 SQL Azure 之前，請確定 SQL Azure 的實例正在執行，而且可以接受連接。  
  
**連接至 SQL Azure**  
  
1.  在 [ **檔案] 功能表上** ，選取 [ **連接到 SQL Azure** (這個選項會在建立專案) 之後啟用。  
  
    如果您先前已連線到 SQL Azure，命令名稱將會 **重新連接至 Sql azure**。  
  
2.  在 [連接] 對話方塊中，輸入或選取 SQL Azure 的伺服器名稱。  
  
3.  輸入，然後選取或 **流覽** 資料庫名稱。  
  
4.  輸入或選取使用者 **名稱**。  
  
5.  輸入 **密碼**。  
  
6.  SSMA 建議對 SQL Azure 進行加密的連接。  
  
7.  按一下 [ **連接**]。  
  
> [!IMPORTANT]  
> 適用于 MySQL 的 SSMA 不支援連接至 SQL Azure 中的 **master** 資料庫。  
  
## <a name="synchronizing-sql-azure-metadata"></a>同步處理 SQL Azure 中繼資料  
Azure SQL Database 中資料庫的相關中繼資料不會自動更新。 當您第一次連線到 SQL Azure 時，或上次手動更新中繼資料時，SQL Azure 中繼資料瀏覽器中的中繼資料是中繼資料的快照集。 您可以手動更新所有資料庫的中繼資料，或任何單一資料庫或資料庫物件的中繼資料。  
  
**若要同步處理中繼資料**  
  
1.  請確定您已連線到 SQL Azure。  
  
2.  在 SQL Azure 中繼資料瀏覽器中，選取您要更新的資料庫或資料庫架構旁的核取方塊。  
  
    例如，若要更新所有資料庫的中繼資料，請選取 [資料庫] 旁的方塊。  
  
3.  以滑鼠右鍵按一下 [資料庫] 或個別的資料庫或資料庫架構，然後選取 [ **與資料庫同步處理**]。  
  
## <a name="next-step"></a>後續步驟  
遷移的下一個步驟取決於您的專案需求：  
  
-   若要自訂 MySQL 架構與 Azure SQL Database 之間的對應，請參閱 [將 Mysql 資料庫對應到 SQL Server 架構 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   若要自訂專案的設定選項，請參閱 [設定專案選項 &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   若要自訂來源和目標資料類型的對應，請參閱將 [MySQL 和 SQL Server 資料類型對應 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   如果您不需要執行上述任何一項工作，您可以將 MySQL 資料庫物件定義轉換成 SQL Azure 物件定義。 如需詳細資訊，請參閱將 [MySQL 資料庫轉換 &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 MySQL 資料庫遷移至 SQL Server Azure SQL Database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
