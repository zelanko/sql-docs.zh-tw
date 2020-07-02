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
ms.openlocfilehash: 905e70c58440b4145af9d7d11783ae5422ef2070
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789219"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  在手動認可模式中，使用開啟的交易在語句控制碼上呼叫**SQLFreeHandle** ，會導致資料庫的暫止變更回復。 在語句控制碼上呼叫**SQLFreeHandle**一律會關閉任何開啟的資料指標，並捨棄暫止的結果，釋放與語句控制碼相關聯的所有資源。  
  
## <a name="see-also"></a>另請參閱  
 [SQLFreeHandle 函式](https://go.microsoft.com/fwlink/?LinkId=59345)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
