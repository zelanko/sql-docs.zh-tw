---
title: "SQL Server 2016 中對於 Database Engine 的重大變更 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/15/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "資料庫引擎 [SQL Server], 新功能"
  - "重大變更 [SQL Server]"
ms.assetid: 47edefbd-a09b-4087-937a-453cd5c6e061
caps.latest.revision: 144
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 144
---
# SQL Server 2016 中對於 Database Engine 的重大變更
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  本主題描述 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] 以及舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的重大變更。 這些變更可能會中斷以舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]為根據的應用程式、指令碼或功能。 當您升級時可能會遇到這些問題。  
  
##  <a name="a-namesql15a-breaking-changes-in-includesssql15tokensssql15mdmd"></a><a name="SQL15"></a> [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 的重大變更  
  
-   sys.dm_io_virtual_file_stats 的 sample_ms 資料行已經從 **int** 擴充到 **bigint** 資料類型。  
  
-   sys.fn_virtualfilestats 的 TimeStamp 資料行已經從 **int** 擴充到 **bigint** 資料類型。  

-   使用 MD2、MD4、MD5、SHA 或 SHA1 雜湊演算法 (不建議使用) 必須將資料庫相容性層級設定為早於 130。  

-   在資料庫相容性層級 130 下，藉由考量小數部分的毫秒從 **datetime** 隱含轉換至 **datetime2** 資料類型顯示改善的精確度，會導致不同的轉換值。 只要 datetime 和 datetime2 資料類型之間存在混合的比較案例，就明確轉換為 datetime2 資料類型。

  
## <a name="previous-versions"></a>先前版本  
  
-   [SQL Server 2014 中對於 Database Engine 的重大變更](https://msdn.microsoft.com/library/ms143179\(v=sql.120\))  
  
-   [SQL Server 2012 中對於 Database Engine 的重大變更](https://msdn.microsoft.com/library/ms143179\(v=sql.110\))  
  
-   [SQL Server 2008 中對於 Database Engine 的重大變更](https://msdn.microsoft.com/library/ms143179\(v=sql.100\))  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2016 中已被取代的 Database Engine 功能](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2016 中已停止的 Database Engine 功能](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [SQL Server Database Engine 回溯相容性](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20Compatibility%20Level%20\(Transact-SQL\).md)  
  
  