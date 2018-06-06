---
title: 擷取結果集資訊 (ODBC) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-how-to
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a75d60fe1175026b8c458d867ad6b528172456e7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="processing-results---retrieve-result-set-information"></a>處理結果集擷取結果集資訊
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
### <a name="to-get-information-about-a-result-set"></a>取得結果集的相關資訊  
  
1.  呼叫[SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md)結果集中取得資料行數目。  
  
2.  對於結果集內的每個資料行：  
  
    -   呼叫[SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)來取得結果資料行的相關資訊。  
  
     或  
  
    -   呼叫[SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)取得結果資料行的特定描述項資訊。  
  
## <a name="see-also"></a>另請參閱  
[處理結果 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[判斷特性的結果集 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
