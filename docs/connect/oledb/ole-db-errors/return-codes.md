---
title: 傳回碼 |Microsoft 文件
description: 傳回碼
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
- OLE DB error handling, return codes
- OLE DB Driver for SQL Server, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: bcc47e5e4cdaffc259ae760fd0e1e2073eb9fab6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="return-codes"></a>傳回碼
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在大部分的基本層級，成員函數不是成功就是失敗。 在更精確一點的層級，函數可能會成功，但是其成功可能不是應用程式開發人員所樂見的。  
  
 如需有關 OLE DB 傳回碼的詳細資訊，請參閱[傳回碼 (OLE DB)](http://go.microsoft.com/fwlink/?LinkId=101631)。  
  
 當 OLE DB 驅動程式的 SQL Server 成員函式傳回 S_OK 時，函數就會成功。  
  
 當 OLE DB 驅動程式的 SQL Server 成員函式沒有傳回 S_OK 時，OLE/COM HRESULT 解開的 FAILED 和 IS_ERROR 巨集可以決定整體成功或失敗函式。  
  
 如果 FAILED 或 IS_ERROR 傳回 TRUE，則 SQL Server 取用者，OLE DB 驅動程式可確保成員函數執行失敗。 當 FAILED 或 IS_ERROR 傳回 FALSE，而且 HRESULT 不等於 S_OK 時，SQL Server 取用者可確保函數在某種意義上會成功，OLE DB 驅動程式。 取用者可以擷取傳回的這個 「 資訊成功 」 從 SQL Server 錯誤的介面，OLE DB 驅動程式的詳細的資訊。 此外，在函數清楚地失敗 （FAILED 巨集會傳回 TRUE） 的情況下，擴充的錯誤資訊是可從 SQL Server 錯誤的介面，OLE DB 驅動程式中。  
  
 OLE DB 驅動程式的 SQL Server 取用者通常會使用資訊的 DB_S_ERRORSOCCURRED 「 成功 」 的 HRESULT 傳回。 傳回 DB_S_ERRORSOCCURRED 的成員函數通常會定義一或多個可提供狀態值給取用者的參數。 沒有錯誤可能會提供資訊給取用者不在狀態值參數中傳回，因此取用者應該實作來擷取狀態值，它們依然可用的應用程式邏輯。  
  
 SQL Server 成員函式，OLE DB 驅動程式不會傳回成功碼 S_FALSE。 所有 OLE DB 驅動程式的 SQL Server 成員函式一律傳回 S_OK 來表示成功。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](../../oledb/ole-db-errors/errors.md)  
  
  
