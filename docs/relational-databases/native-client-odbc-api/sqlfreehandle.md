---
title: SQLFreeHandle |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fc8a8cac364c9226d32ed2ebadbc2702e13031ab
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298441"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在手動認可模式中，使用開啟的交易在語句控制碼上呼叫**SQLFreeHandle** ，會導致資料庫的暫止變更回復。 在語句控制碼上呼叫**SQLFreeHandle**一律會關閉任何開啟的資料指標，並捨棄暫止的結果，釋放與語句控制碼相關聯的所有資源。  
  
## <a name="see-also"></a>另請參閱  
 [SQLFreeHandle 函式](https://go.microsoft.com/fwlink/?LinkId=59345)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
