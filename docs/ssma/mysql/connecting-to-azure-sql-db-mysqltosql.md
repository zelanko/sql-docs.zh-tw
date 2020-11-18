---
description: '連接至 Azure SQL Database (MySQLToSQL) '
title: 連接至 Azure SQL Database (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 11/16/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to Azure SQL Database, SQL Azure permissions
- Connecting to Azure SQL Database, synchronization
ms.assetid: d0b6f16a-1880-459d-a0c7-28b7ef15c56a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 6604d35058c9e8876638beee3ec6d73a9cd7a491
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870086"
---
# <a name="connecting-to-azure-sql-database-mysqltosql"></a>連接至 Azure SQL Database (MySQLToSQL) 

若要將 MySQL 資料庫遷移至 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ，您必須連接到的目標實例 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 。 當您連接時，SSMA 會取得實例中所有資料庫的相關中繼資料 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ，並在 **Azure SQL Database 中繼資料瀏覽器** 中顯示資料庫中繼資料。 SSMA 會儲存您所連接之實例的資訊 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ，但不會儲存密碼。

您的連接 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 會保持作用中，直到您關閉專案為止。 當您重新開啟專案時， [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 如果您想要使用中的伺服器連接，則必須重新連接到。 您可以離線工作，直到您將資料庫物件載入 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 並遷移資料為止。

有關實例的中繼資料 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 不會自動同步處理。 相反地，若要更新 **Azure SQL Database 中繼資料瀏覽器** 中的中繼資料，您必須手動更新 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 中繼資料。 如需詳細資訊，請參閱本主題稍後的「同步處理 Azure SQL Database 中繼資料」一節。

## <a name="required-azure-sql-database-permissions"></a>必要的 Azure SQL Database 許可權

用來連接的帳戶 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 需要不同的許可權，視帳戶執行的動作而定：

- 若要將 MySQL 物件轉換成 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法、從更新中繼資料 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ，或將轉換的語法儲存至腳本，此帳戶必須具有登入實例的許可權 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 。

- 若要將資料庫物件載入至 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ，帳戶必須是 **db_ddladmin** 資料庫角色的成員。

- 若要將資料移轉至 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ，帳戶必須是 **db_owner** 資料庫角色的成員。

## <a name="establishing-an-azure-sql-database-connection"></a>建立 Azure SQL Database 連接

將 MySQL 資料庫物件轉換成 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 語法之前，您必須建立與實例的連接，以便將 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] mysql 資料庫移轉至其中。

當您定義連接屬性時，您也會指定要遷移物件和資料的資料庫。 連接至之後，您可以在 MySQL 架構層級自訂此對應 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 。 如需詳細資訊，請參閱 [將 MySQL 資料庫對應至 SQL Server 架構 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)。

> [!IMPORTANT]
> 在您嘗試連接到之前 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ，請確定您的 IP 位址允許透過 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 防火牆。

連線至 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]：

1. 在 [檔案] **功能表上** ，選取 [ **連接到 Azure SQL Database** (這個選項會在建立專案) 之後啟用。
   如果您先前已連線到 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ，命令名稱將會 **重新連接到 Azure SQL Database**。

2. 在 [連接] 對話方塊中，輸入或選取的伺服器名稱 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 。

3. 輸入，然後選取或 **流覽** 資料庫名稱。

4. 輸入或選取使用者 **名稱**。

5. 輸入 **密碼**。

6. SSMA 建議的加密連接 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 。

7. 按一下 [ **連接**]。
  
## <a name="synchronizing-azure-sql-database-metadata"></a>同步處理 Azure SQL Database 中繼資料

中資料庫的相關中繼資料 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 不會自動更新。 當您第一次連接或上次手動更新中繼資料時， **Azure SQL Database Metadata Explorer** 中的中繼資料是中繼資料的快照集 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 。 您可以手動更新所有資料庫的中繼資料，或任何單一資料庫或資料庫物件的中繼資料。 若要同步處理中繼資料：

1. 請確定您已連接到 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 。

2. 在 **Azure SQL Database 中繼資料瀏覽器**] 中，選取您要更新的資料庫或資料庫架構旁的核取方塊。
   例如，若要更新所有資料庫的中繼資料，請選取 [ **資料庫**] 旁的方塊。

3. 以滑鼠右鍵按一下 [ **資料庫**] 或個別的資料庫或資料庫架構，然後選取 [ **與資料庫同步處理**]。

## <a name="next-step"></a>後續步驟

遷移的下一個步驟取決於您的專案需求：

- 若要自訂 MySQL 架構與之間的對應 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ，請參閱 [將 Mysql 資料庫對應至 SQL Server 架構 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)。
- 若要自訂專案的設定選項，請參閱 [&#40;MySQLToSQL&#41;設定專案選項 ](../../ssma/mysql/setting-project-options-mysqltosql.md)。
- 若要自訂來源和目標資料類型的對應，請參閱將 [MySQL 和 SQL Server 資料類型對應 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)。
- 如果您不需要執行上述任何一項工作，您可以將 MySQL 資料庫物件定義轉換成 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 物件定義。 如需詳細資訊，請參閱將 [MySQL 資料庫轉換 &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)。

## <a name="see-also"></a>另請參閱

[將 MySQL 資料庫遷移至 SQL Server Azure SQL Database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)
