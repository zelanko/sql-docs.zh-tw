---
title: SQL Server 訊息結果 |Microsoft 文件
description: SQL Server 訊息結果
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 586926250d1234c15cc77511800105b2c58f1e60
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-message-results"></a>SQL Server 訊息結果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  下列[!INCLUDE[tsql](../../../includes/tsql-md.md)]陳述式並不會產生 OLE DB 驅動程式的 SQL Server 資料列集或執行時，受影響資料列計數：  
  
-   PRINT  
  
-   具有 10 或更低嚴重性的 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 這些陳述式會傳回一或多個參考用訊息，或使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 傳回參考用訊息來取代資料列集或計數結果。 在成功執行，SQL Server OLE DB 驅動程式傳回 S_OK，而且訊息可以提供給 SQL Server 取用者，OLE DB 驅動程式。  
  
 SQL Server OLE DB 驅動程式會傳回 S_OK，而且有一個或多個參考用訊息可取得在執行許多[!INCLUDE[tsql](../../../includes/tsql-md.md)]陳述式或 SQL Server 成員函式的 OLE DB 驅動程式的取用者執行。  
  
 允許動態指定查詢文字的 SQL Server 取用者，OLE DB 驅動程式應該檢查錯誤介面值為何傳回碼、 組態選項或傳回的每個成員函數執行之後**IRowset**或**IMultipleResults**介面參考或受影響的資料列計數。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](../../oledb/ole-db-errors/errors.md)  
  
  
