---
title: 將 Oracle 資料庫移轉至 SQL Server (OracleToSQL) |Microsoft Docs
description: 使用這個建議的程式，將 Oracle 資料庫移轉至 SQL Server 或 Azure SQL Database 使用 SQL Server 移轉小幫手 (SSMA) 。
ms.prod: sql
ms.custom: ''
ms.date: 04/22/2018
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1d196dd6-4322-4c98-bb72-602c57d96134
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 194d33d0b5318ca66494b838c7f59dfde5c72b88
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87933439"
---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>將 Oracle 資料庫移轉到 SQL Server (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 適用于 Oracle 的 Migration Assistant (SSMA) 是全方位的環境，可協助您快速將 Oracle 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、Azure SQL Database 或 AZURE SQL 資料倉儲。 您可以使用 SSMA for Oracle 來查看資料庫物件和資料、評估要遷移的資料庫、將資料庫物件遷移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、Azure SQL Database 或 AZURE Sql 資料倉儲，然後將資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、Azure SQL Database 或 Azure Sql 資料倉儲。 請注意，您無法遷移 SYS 和系統 Oracle 架構。
  
## <a name="recommended-migration-process"></a>建議的遷移程式  
若要成功將物件和資料從 Oracle 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、Azure SQL Database 或 AZURE SQL 資料倉儲，請使用下列程式：
  
1.  [建立新的 SSMA 專案](working-with-ssma-projects-oracletosql.md)。  
  
    建立專案之後，您可以設定專案轉換、遷移和類型對應選項。 如需專案設定的詳細資訊，請參閱 [&#40;OracleToSQL&#41;設定專案選項 ](../../ssma/oracle/setting-project-options-oracletosql.md)。 如需有關如何自訂資料類型對應的詳細資訊，請參閱將 [Oracle 和 SQL Server 資料類型對應 &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)。  
  
2.  [連接到 Oracle 資料庫伺服器](connecting-to-oracle-database-oracletosql.md)。  
  
3.  [連接到 SQL Server 的實例](connecting-to-sql-server-oracletosql.md)。  
  
4.  [將 Oracle 資料庫架構對應至 SQL Server 資料庫架構](mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md)。  
  
5.  （選擇性） [建立評量報告](assessing-oracle-schemas-for-conversion-oracletosql.md) 以評估資料庫物件的轉換，並估計轉換時間。  
  
6.  [將 Oracle 資料庫架構轉換成 SQL Server 架構](converting-oracle-schemas-oracletosql.md)。  
  
7.  [將轉換的資料庫物件載入 SQL Server 中](loading-converted-database-objects-into-sql-server-oracletosql.md)。  
  
    您可以透過下列其中一種方式來執行此動作：  
  
    -   儲存並執行腳本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
    -   同步處理資料庫物件。  
  
8.  [將資料移轉至 SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md)。  
  
9. 如有必要，請更新資料庫應用程式。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[使用 SSMA for Oracle 進行消費者入門 &#40;OracleToSQL&#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  
