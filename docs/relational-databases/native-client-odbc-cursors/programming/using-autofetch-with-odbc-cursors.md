---
title: "使用自動擷取搭配 ODBC 資料指標 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, autofetch
- autofetch option
- cursors [ODBC], autofetch
ms.assetid: 57bd55f4-8945-4d8d-9f58-d30c81d2a514
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9b0dd154b1f8a4dd791dfc111dacaa750a66da96
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="using-autofetch-with-odbc-cursors"></a>使用自動擷取搭配 ODBC 資料指標
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  當連接到的執行個體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式在使用任何伺服器資料指標類型時支援自動擷取選項。 使用自動擷取， **SQLExecute**或**SQLExecDirect**開啟資料指標的函式也具有隱含[SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)(SQL_FIRST) 函數。 構成第一個資料列集的資料列會當做陳述式執行的一部分而傳回至繫結的應用程式變數，如此就不需要再一次透過網路往返伺服器。 [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)時不支援已啟用自動擷取選項; 將結果集資料行必須繫結至程式變數。  
  
 應用程式會藉由將驅動程式特定的 SQL_SOPT_SS_CURSOR_OPTIONS 陳述式屬性設定為 SQL_CO_AF 來要求自動擷取。  
  
## <a name="see-also"></a>另請參閱  
 [資料指標程式設計詳細資料 &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
