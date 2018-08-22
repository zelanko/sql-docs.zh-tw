---
title: 移轉的 Oracle 資料庫到 SQL Server (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 04/22/2018
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1d196dd6-4322-4c98-bb72-602c57d96134
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 05cdf94aaac3c3b5401681edb996ed740fbc94a6
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395522"
---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>將 Oracle 資料庫移轉到 SQL Server (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移轉小幫手 (SSMA) for Oracle 是完整的環境，可協助您快速 Oracle 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，Azure SQL DB 或 Azure SQL 資料倉儲。 您可以藉由使用 SSMA for Oracle，檢閱資料庫物件和資料、 評估要移轉的資料庫，資料庫將物件移轉為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，Azure SQL DB 或 Azure SQL 資料倉儲，然後再移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，Azure SQL DB 或 Azure SQL 資料倉儲。 請注意您無法將 SYS 和系統 Oracle 結構描述移轉。
  
## <a name="recommended-migration-process"></a>建議的移轉程序  
若要成功移轉物件和資料，從 Oracle 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，Azure SQL DB 或 Azure SQL 資料倉儲，請使用下列程序：
  
1.  [建立新的 SSMA 專案](working-with-ssma-projects-oracletosql.md)。  
  
    建立專案之後，您可以設定專案轉換、 移轉和型別對應的選項。 專案設定的相關資訊，請參閱[設定專案選項&#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md)。 如需如何自訂資料型別對應資訊，請參閱[對應 Oracle 和 SQL Server 資料類型&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)。  
  
2.  [連接到 Oracle 資料庫伺服器](connecting-to-oracle-database-oracletosql.md)。  
  
3.  [連接到 SQL server 執行個體](connecting-to-sql-server-oracletosql.md)。  
  
4.  [將 Oracle 資料庫結構描述對應至 SQL Server 資料庫結構描述](mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md)。  
  
5.  （選擇性）[建立評定報表](assessing-oracle-schemas-for-conversion-oracletosql.md)評估進行轉換的資料庫物件，並且估計的轉換時間。  
  
6.  [將 Oracle 資料庫結構描述轉換成 SQL Server 結構描述](converting-oracle-schemas-oracletosql.md)。  
  
7.  [已轉換的資料庫物件載入 SQL Server](loading-converted-database-objects-into-sql-server-oracletosql.md)。  
  
    您可以透過下列方式之一來這麼做：  
  
    -   儲存指令碼，並在執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
    -   同步處理資料庫物件。  
  
8.  [將資料移轉至 SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md)。  
  
9. 如有必要，更新資料庫的應用程式。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[開始使用 SSMA for Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  
