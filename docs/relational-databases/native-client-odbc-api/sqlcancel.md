---
title: "SQLCancel |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
caps.latest.revision: "5"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7b959ce4ef5f0eb7298f7203401fa6be6c96581d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="sqlcancel"></a>SQLCancel
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516)主題指出，在 ODBC 2.x 中，如果應用程式呼叫**SQLCancel**當陳述式，不進行任何處理**SQLCancel**具有相同的效果**SQLFreeStmt**與**SQL_CLOSE**選項; 這種行為只為完整性而定義，而且應用程式應該呼叫**SQLFreeStmt**或**SQLCloseCursor**來關閉資料指標。 不過，即使您[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端應用程式設定的 ODBC API 版本為 3.5.x 或更新版本， **SQLCancel**函式會使用 ODBC 2.x 行為。  
  
## <a name="see-also"></a>請參閱  
 [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
