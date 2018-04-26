---
title: 移轉的 Oracle 資料庫到 SQL Server (OracleToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 04/22/2018
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1d196dd6-4322-4c98-bb72-602c57d96134
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Active
ms.openlocfilehash: 09fe8820413108e4df6479b0a7c2bd95f1f84741
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>將 Oracle 資料庫移轉至 SQL Server (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 移轉小幫手 (SSMA) for Oracle 是一種完整的環境，可協助您快速 Oracle 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，Azure SQL DB、 或 Azure SQL 資料倉儲。 利用 SSMA for Oracle，檢閱資料庫物件和資料，評估要移轉的資料庫，資料庫將物件移轉為[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，Azure SQL DB、 或 Azure SQL 資料倉儲，然後再移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，Azure SQL DB、 或 Azure SQL 資料倉儲。 請注意您無法移轉 SYS 和系統 Oracle 結構描述。
  
## <a name="recommended-migration-process"></a>建議您移轉程序  
若要成功移轉物件和資料，從 Oracle 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，Azure SQL DB、 或 Azure SQL 資料倉儲，使用下列程序：
  
1.  [建立新的 SSMA 專案](http://msdn.microsoft.com/en-us/ee5d94c0-c7a6-4779-bd32-729bdaf61e1b)。  
  
    建立專案之後，您可以設定專案轉換、 移轉和型別對應的選項。 專案設定的相關資訊，請參閱[設定專案選項&#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md)。 如需如何自訂資料型別對應資訊，請參閱[對應 Oracle 和 SQL Server 資料類型&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)。  
  
2.  [連接到 Oracle 資料庫伺服器](http://msdn.microsoft.com/en-us/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6)。  
  
3.  [連接到 SQL server 執行個體](http://msdn.microsoft.com/en-us/1b2a8059-1829-4904-a82f-9c06de1e245f)。  
  
4.  [Oracle 資料庫結構描述對應到 SQL Server 資料庫結構描述](http://msdn.microsoft.com/en-us/0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc)。  
  
5.  （選擇性）[建立的評估報告](http://msdn.microsoft.com/en-us/4de9bcf6-1346-4740-87f9-7f24a8226357)以評估資料庫物件的轉換，並評估的轉換時間。  
  
6.  [將 Oracle 資料庫結構描述轉換成 SQL Server 結構描述](http://msdn.microsoft.com/en-us/e021182d-31da-443d-b110-937f5db27272)。  
  
7.  [轉換的資料庫物件載入 SQL Server](http://msdn.microsoft.com/en-us/a8ae33b2-1883-4785-922b-ea0e31c0b37a)。  
  
    您可以下列方式之一：  
  
    -   儲存指令碼，執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
    -   同步處理資料庫物件。  
  
8.  [將資料移轉到 SQL Server](http://msdn.microsoft.com/en-us/e23c5268-41ed-4e55-9fe7-a11376202a13)。  
  
9. 如有必要，更新資料庫的應用程式。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[開始使用 SSMA for Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  
