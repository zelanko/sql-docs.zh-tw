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
ms.openlocfilehash: f20b7271932cbbcc0538fc9923e45b2fc029f646
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38983200"
---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>將 Oracle 資料庫移轉至 SQL Server (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 移轉小幫手 (SSMA) for Oracle 是完整的環境，可協助您快速 Oracle 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，Azure SQL DB 或 Azure SQL 資料倉儲。 您可以藉由使用 SSMA for Oracle，檢閱資料庫物件和資料、 評估要移轉的資料庫，資料庫將物件移轉為[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，Azure SQL DB 或 Azure SQL 資料倉儲，然後再移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，Azure SQL DB 或 Azure SQL 資料倉儲。 請注意您無法將 SYS 和系統 Oracle 結構描述移轉。
  
## <a name="recommended-migration-process"></a>建議的移轉程序  
若要成功移轉物件和資料，從 Oracle 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，Azure SQL DB 或 Azure SQL 資料倉儲，請使用下列程序：
  
1.  [建立新的 SSMA 專案](http://msdn.microsoft.com/ee5d94c0-c7a6-4779-bd32-729bdaf61e1b)。  
  
    建立專案之後，您可以設定專案轉換、 移轉和型別對應的選項。 專案設定的相關資訊，請參閱[設定專案選項&#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md)。 如需如何自訂資料型別對應資訊，請參閱[對應 Oracle 和 SQL Server 資料類型&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)。  
  
2.  [連接到 Oracle 資料庫伺服器](http://msdn.microsoft.com/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6)。  
  
3.  [連接到 SQL server 執行個體](http://msdn.microsoft.com/1b2a8059-1829-4904-a82f-9c06de1e245f)。  
  
4.  [將 Oracle 資料庫結構描述對應至 SQL Server 資料庫結構描述](http://msdn.microsoft.com/0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc)。  
  
5.  （選擇性）[建立評定報表](http://msdn.microsoft.com/4de9bcf6-1346-4740-87f9-7f24a8226357)評估進行轉換的資料庫物件，並且估計的轉換時間。  
  
6.  [將 Oracle 資料庫結構描述轉換成 SQL Server 結構描述](http://msdn.microsoft.com/e021182d-31da-443d-b110-937f5db27272)。  
  
7.  [已轉換的資料庫物件載入 SQL Server](http://msdn.microsoft.com/a8ae33b2-1883-4785-922b-ea0e31c0b37a)。  
  
    您可以透過下列方式之一來這麼做：  
  
    -   儲存指令碼，並在執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
    -   同步處理資料庫物件。  
  
8.  [將資料移轉至 SQL Server](http://msdn.microsoft.com/e23c5268-41ed-4e55-9fe7-a11376202a13)。  
  
9. 如有必要，更新資料庫的應用程式。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[開始使用 SSMA for Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  
