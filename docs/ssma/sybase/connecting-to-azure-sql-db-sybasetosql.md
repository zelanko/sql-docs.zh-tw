---
description: '連接至 Azure SQL Database (SybaseToSQL) '
title: 連接至 Azure SQL Database (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: eacdca6cf260557171f5adf63f8590842de77fcb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88372344"
---
# <a name="connecting-to-azure-sql-database-sybasetosql"></a>連接至 Azure SQL Database (SybaseToSQL) 
若要將 Sybase 資料庫移轉至 Azure SQL Database，您必須連接到 Azure SQL Database 的目標實例。 當您連接時，SSMA 會取得 Azure SQL Database 實例中所有資料庫的相關中繼資料，並在 Azure SQL Database 中繼資料瀏覽器中顯示資料庫中繼資料。 SSMA 會儲存您所連接之 Azure SQL Database 實例的資訊，但不會儲存密碼。  
  
您的 Azure SQL Database 連接會保持作用中，直到您關閉專案為止。 當您重新開啟專案時，如果您想要使用伺服器的使用中連接，則必須重新連接到 Azure SQL Database。 您可以離線工作，直到將資料庫物件載入 Azure SQL Database 並遷移資料為止。  
  
Azure SQL Database 實例的中繼資料不會自動同步處理。 相反地，若要更新 Azure SQL Database 中繼資料瀏覽器中的中繼資料，您必須手動更新 Azure SQL Database 中繼資料。 如需詳細資訊，請參閱本主題稍後的「同步處理 Azure SQL Database 中繼資料」一節。  
  
## <a name="required-azure-sql-database-permissions"></a>必要的 Azure SQL Database 許可權  
用來連接 Azure SQL Database 的帳戶需要不同的許可權，視帳戶執行的動作而定：  
  
1.  若要將 Sybase 物件轉換成 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法、更新 Azure SQL Database 的中繼資料，或將轉換的語法儲存至腳本，此帳戶必須具有登入 Azure SQL Database 實例的許可權。  
  
2.  若要將資料庫物件載入 Azure SQL Database 中，最低許可權需求是目標資料庫中  **db_owner** 資料庫角色的成員資格。  
  
## <a name="establishing-an-azure-sql-database-connection"></a>建立 Azure SQL Database 連接  
將 Sybase 資料庫物件轉換成 Azure SQL Database 語法之前，您必須建立與您要遷移 Sybase 資料庫之 Azure SQL Database 實例的連接。  
  
當您定義連接屬性時，您也會指定要遷移物件和資料的資料庫。 您可以在連接到 Azure SQL Database 之後，于 Sybase 架構層級自訂此對應。 如需詳細資訊，請參閱 [將 SYBASE ASE 架構對應至 SQL Server 架構 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
> [!WARNING]  
> 在您嘗試連接到 Azure SQL Database 之前，請確定 Azure SQL Database 的實例正在執行，而且可以接受連接。  
  
**連接到 Azure SQL Database**  
  
1.  在 [檔案] **功能表上** ，選取 [ **連接到 Azure SQL Database** (這個選項會在建立專案) 之後啟用。  
  
    如果您先前已連線到 Azure SQL Database，命令名稱將會 **重新連接到 Azure SQL Database**  
  
2.  在 [連接] 對話方塊中，輸入或選取 Azure SQL Database 的伺服器名稱。  
  
3.  輸入，然後選取或 **流覽** 資料庫名稱。  
  
4.  輸入或選取使用者 **名稱**。  
  
5.  輸入 **密碼**。  
  
6.  SSMA 建議 Azure SQL Database 的加密連接。  
  
7.  按一下 [ **連接**]。  
  
> [!IMPORTANT]  
> SSMA for Sybase 不支援連接到 Azure SQL Database 中的 **master** 資料庫。  
  
## <a name="synchronizing-azure-sql-database-metadata"></a>同步處理 Azure SQL Database 中繼資料  
Azure SQL Database 資料庫的相關中繼資料不會自動更新。 當您第一次連接到 Azure SQL Database，或上次手動更新中繼資料時，Azure SQL Database 中繼資料瀏覽器中的中繼資料是中繼資料的快照集。 您可以手動更新所有資料庫的中繼資料，或任何單一資料庫或資料庫物件的中繼資料。  
  
**若要同步處理中繼資料**  
  
1.  請確定您已連線到 Azure SQL Database。  
  
2.  在 Azure SQL Database 中繼資料瀏覽器] 中，選取您要更新的資料庫或資料庫架構旁的核取方塊。  
  
    例如，若要更新所有資料庫的中繼資料，請選取 [資料庫] 旁的方塊。  
  
3.  以滑鼠右鍵按一下 [資料庫] 或個別的資料庫或資料庫架構，然後選取 [ **與資料庫同步處理**]。  
  
## <a name="next-step"></a>後續步驟  
遷移的下一個步驟取決於您的專案需求：  
  
-   若要自訂 Sybase 架構與 Azure SQL Database 資料庫與架構之間的對應，請參閱 [將 SYBASE ASE 架構對應至 SQL Server 架構 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
-   若要自訂專案的設定選項，請參閱 [設定專案選項 &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)  
  
-   若要自訂來源和目標資料類型的對應，請參閱 [對應 SYBASE ASE 和 SQL Server 資料類型 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)  
  
-   如果您不需要執行上述任何一項工作，您可以將 Sybase 資料庫物件定義轉換成 Azure SQL Database 物件定義。 如需詳細資訊，請參閱 [轉換 SYBASE ASE 資料庫物件 &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Sybase ASE 資料庫移轉至 SQL Server Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
