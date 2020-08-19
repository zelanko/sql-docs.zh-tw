---
description: 使用資料檔案與格式檔案
title: 使用資料檔案和格式檔案 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], file formats
- ODBC, functions
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [SQL Server Native Client]
- ODBC, bulk copy operations
- bulk copy [ODBC], data files
ms.assetid: c01b7155-3f0a-473d-90b7-87a97bc56ca5
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7a71502f608c1e283831bfb43f80aab6727bd77a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448610"
---
# <a name="using-data-files-and-format-files"></a>使用資料檔案與格式檔案
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  最簡單的大量複製程式會執行下列動作：  
  
1.  呼叫 [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) 來指定大量複製 (將 BCP_OUT) 從資料表或 view 移至資料檔案。  
  
2.  呼叫 [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) ，以執行大量複製作業。  
  
 資料檔案是在原生模式下建立的，因此，來自資料表或檢視之所有資料行的資料會以與資料庫相同的格式，儲存在資料檔案中。 接著，可以使用這些相同的步驟，並設定 DB_IN (而非 DB_OUT)，將檔案大量複製到伺服器中。 只有當來源資料表和目標資料表兩者都具有相同的結構時，才適用這種方法。 您也可以使用 **/n** (原生模式) 參數，將產生的資料檔案輸入至**bcp**公用程式。  
  
 大量複製 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的結果集，而非直接從資料表或檢視大量複製：  
  
1.  呼叫 **bcp_init** 指定大量複製，但為數據表名稱指定 Null。  
  
2.  呼叫 [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) ，並將 *EOPTION* 設定為 BCPHINTS，並將 *iValue* 設定為包含 transact-sql 語句之 SQLTCHAR 字串的指標。  
  
3.  呼叫 **bcp_exec** ，以執行大量複製作業。  

 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式可能是會產生結果集的任何陳述式。 系統會建立包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式第一個結果集的資料檔案。 如果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式產生多個結果集，則大量複製會忽略第一個結果集後的任何結果集。  
  
 若要建立資料行資料的資料檔案，其資料行資料的儲存方式與資料表的格式不同，請呼叫 [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) 指定要變更的資料行數目，然後針對您想要變更其格式的每個資料行呼叫 [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md) 。 這是在呼叫 **bcp_init** 之後，但在呼叫 **bcp_exec**之前完成的。 **bcp_colfmt** 指定資料行資料儲存在資料檔案中的格式。 當大量複製時，可以使用它。您也可以使用 **bcp_colfmt** 來設定資料列和資料行結束字元。 例如，如果您的資料不包含任何定位字元，則可以使用 **bcp_colfmt** 將定位字元設定為每個資料行的結束字元，藉以建立 tab 字元分隔的檔案。  
  
 大量複製和使用**bcp_colfmt**時，您可以輕鬆地建立格式檔案，以描述上次呼叫**bcp_colfmt**之後呼叫[bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md)所建立的資料檔案。  
  
 從格式檔案所描述的資料檔大量複製時，請在**bcp_init**之後，但在**bcp_exec**之前呼叫[bcp_readfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md) ，以讀取格式檔案。  
  
 從資料檔案大量複製到時， **bcp_control** 函數會控制數個選項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 **bcp_control** 設定選項，例如終止前的錯誤最大數目、開始大量複製之檔案中的資料列、要停止的資料列，以及批次大小。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行大量複製作業 ](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
