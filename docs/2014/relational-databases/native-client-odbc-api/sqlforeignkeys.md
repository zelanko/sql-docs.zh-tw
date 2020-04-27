---
title: SQLForeignKeys |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLForeignKeys function
ms.assetid: 6c01ce0d-30d7-4c86-8705-3ab254d8a845
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8481b0f19566ed0e55f31480f9ab8be0c9441c7d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63184473"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援串聯更新，而且會透過外部索引鍵條件約束機制刪除。 如果在 FOREIGN KEY 條件約束的 ON UPDATE 和/或 ON DELETE 子句上指定 CASCADE 選項，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對 UPDATE_RULE 和/或 DELETE_RULE 資料行傳回 SQL_NO_ACTION。 如果在 FOREIGN KEY 條件約束的 ON UPDATE 和/或 ON DELETE 子句上指定 NO ACTION 選項，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對 UPDATE_RULE 和/或 DELETE_RULE 資料行傳回 SQL_NO_ACTION。  
  
 當任何**SQLForeignKeys**參數中出現不正確值時， **SQLForeignKeys**會在執行時傳回 SQL_SUCCESS。 當這些參數中使用了不正確值時， **SQLFetch**會傳回 SQL_NO_DATA。  
  
 **SQLForeignKeys**可以在靜態伺服器資料指標上執行。 嘗試在可更新的（動態或索引鍵集）資料指標上執行**SQLForeignKeys**時，會傳回 SQL_SUCCESS_WITH_INFO，表示資料指標類型已變更。  
  
 Native Client ODBC 驅動程式藉由接受*FKCatalogName*和*sqlforeignkeys*參數的兩部分名稱，支援連結伺服器上之資料表的報告資訊： *Linked_Server_Name. Catalog_Name。* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [SQLForeignKeys 函式](https://go.microsoft.com/fwlink/?LinkId=59344)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
