---
title: 使用資料檔案與格式檔案 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f4c377bbfbe4170b5631ba1ac9c017af1176b279
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63013973"
---
# <a name="using-data-files-and-format-files"></a>使用資料檔案與格式檔案
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  最簡單的大量複製程式會執行下列動作：  
  
1.  呼叫[bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)指定大量複製 （設定 BCP_OUT） 從資料表或檢視，以將資料檔。  
  
2.  呼叫[bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)以便執行大量複製作業。  
  
 資料檔案是在原生模式下建立的，因此，來自資料表或檢視之所有資料行的資料會以與資料庫相同的格式，儲存在資料檔案中。 接著，可以使用這些相同的步驟，並設定 DB_IN (而非 DB_OUT)，將檔案大量複製到伺服器中。 只有當來源資料表和目標資料表兩者都具有相同的結構時，才適用這種方法。 產生的資料檔案也可以輸入要**bcp**公用程式利用 **/n** （原生模式） 參數。  
  
 大量複製 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的結果集，而非直接從資料表或檢視大量複製：  
  
1.  呼叫**bcp_init**來指定大量複製，但是資料表名稱指定 NULL。  
  
2.  呼叫[bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)具有*eOption*設定為 BCPHINTS 並*iValue*設為包含 TRANSACT-SQL 陳述式之 SQLTCHAR 字串的指標。  
  
3.  呼叫**bcp_exec**以便執行大量複製作業。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式可能是會產生結果集的任何陳述式。 系統會建立包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式第一個結果集的資料檔案。 如果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式產生多個結果集，則大量複製會忽略第一個結果集後的任何結果集。  
  
 若要建立哪一個資料行中資料會儲存在不同的格式比資料表中的資料檔案，請呼叫[bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)若要指定資料行數目將會變更，然後呼叫[bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)每個資料行的格式您想要變更。 這完成之後呼叫**bcp_init**但再呼叫**bcp_exec**。 **bcp_colfmt**指定資料行的資料儲存在資料檔中的格式。 大量複製縮小或相應放大時可以使用它。您也可以使用**bcp_colfmt**來設定資料列和資料行結束字元。 比方說，如果您的資料不包含定位字元，您可以建立 tab 鍵分隔的檔案使用**bcp_colfmt**將定位字元設定為每個資料行的結束字元。  
  
 當大量複製以及使用**bcp_colfmt**，您可以輕鬆地建立格式檔案描述您所建立之資料檔案[bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md)最後一個呼叫之後**bcp_colfmt**.  
  
 進行大量複製時從資料檔所使用格式檔案描述，請藉由呼叫讀取格式檔案[bcp_readfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)之後**bcp_init**之前**bcp_exec**。  
  
 **Bcp_control**函數會控制數個選項，當大量複製到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]從資料檔。 **bcp_control**設定的選項包括終止前的錯誤、 開始大量複製、 停止、 資料列和批次大小的檔案中的資料列的最大數目。  
  
## <a name="see-also"></a>另請參閱  
 [執行大量複製作業&#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
