---
description: 處理結果 - 擷取結果集資訊
title: 取出 (ODBC) 的結果集資訊 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 072747868ddd3358c0cc074e16ba64ff4afe980d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490837"
---
# <a name="processing-results---retrieve-result-set-information"></a>處理結果 - 擷取結果集資訊
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
### <a name="to-get-information-about-a-result-set"></a>取得結果集的相關資訊  
  
1.  呼叫 [SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md) 以取得結果集內的資料行數目。  
  
2.  對於結果集內的每個資料行：  
  
    -   呼叫 [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) 以取得結果資料行的相關資訊。  
  
     Or  
  
    -   呼叫 [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) 以取得有關結果資料行的特定描述項資訊。  
  
## <a name="see-also"></a>另請參閱  
[&#40;ODBC&#41;處理結果 ](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[判斷結果集的特性 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
