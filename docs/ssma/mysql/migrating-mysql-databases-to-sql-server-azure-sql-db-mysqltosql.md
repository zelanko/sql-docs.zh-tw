---
title: "將 MySQL 資料庫移轉至 SQL Server-Azure SQL DB |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 8006f9a0-394d-4238-8dc5-44255134628b
caps.latest.revision: "12"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c58cd08cddd34bccaabdfe35004a768c4ad85a2e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="migrating-mysql-databases-to-sql-server---azure-sql-db-mysqltosql"></a>將 MySQL 資料庫移轉至 SQL Server-Azure SQL DB (MySQLToSql)
SQL Server 移轉小幫手 (SSMA) 的 MySQL 是完整的環境，可協助您快速將 MySQL 資料庫移轉至 SQL Server 或 SQL Azure。 利用 SSMA for MySQL，您可以檢視資料庫物件和資料、 評估要移轉的資料庫、 將資料庫物件移轉至 SQL Server 或 SQL Azure，然後將資料移轉到 SQL Server 或 SQL Azure。  
  
## <a name="recommended-migration-process"></a>建議您移轉程序  
若要成功移轉物件和資料從 MySQL 資料庫到 SQL Server 或 SQL Azure，使用下列程序：  
  
1.  [使用 SSMA 專案 &#40;MySQLToSQL &#41;](../../ssma/mysql/working-with-ssma-projects-mysqltosql.md).  
  
    建立專案之後，您可以設定專案轉換、 移轉和型別對應的選項。 如需專案設定的詳細資訊，請參閱[設定專案選項 &#40;MySQLToSQL &#41;](../../ssma/mysql/setting-project-options-mysqltosql.md). 如需如何自訂資料型別對應資訊，請參閱[對應 MySQL 及 SQL Server 資料類型 &#40;MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
2.  [連接到 MySQL &#40;MySQLToSQL &#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
3.  [連接到 SQL Server &#40;MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
4.  [將 MySQL 資料庫對應至 SQL Server 結構描述 &#40;MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
5.  [連接到 Azure SQL DB &#40;MySQLToSQL &#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
6.  （選擇性）[轉換 &#40; 評估 MySQL 資料庫MySQLToSQL &#41;](../../ssma/mysql/assessing-mysql-databases-for-conversion-mysqltosql.md)以評估資料庫物件的轉換，並評估的轉換時間。  
  
7.  [轉換的 MySQL 資料庫 &#40;MySQLToSQL &#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
8.  [同步處理](http://msdn.microsoft.com/en-us/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
9. 您可以下列方式之一：  
  
    -   儲存指令碼和 SQL Server 或 SQL Azure 上執行。  
  
    -   同步處理資料庫物件。  
  
10. [將 MySQL 資料移轉到 SQL Server-Azure SQL DB &#40;MySQLToSQL &#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
11. 如有必要，更新資料庫的應用程式。  
  
> [!NOTE]  
> 您無法移轉 Information_schema 和 MySQL 結構描述。  
  
## <a name="see-also"></a>請參閱＜  
[安裝 SSMA for MySQL &#40;MySqlToSql &#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
[開始使用 SSMA for MySQL &#40;MySQLToSQL &#41;](../../ssma/mysql/getting-started-with-ssma-for-mysql-mysqltosql.md)  
  
