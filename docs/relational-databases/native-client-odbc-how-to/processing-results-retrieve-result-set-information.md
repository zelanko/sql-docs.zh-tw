---
title: 擷取結果集資訊 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2211e77ed927c9c2bb5fd9cc3e5df89bc20a5245
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430247"
---
# <a name="processing-results---retrieve-result-set-information"></a>處理結果-擷取結果集資訊
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
### <a name="to-get-information-about-a-result-set"></a>取得結果集的相關資訊  
  
1.  呼叫[SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md)取得結果集中的資料行數目。  
  
2.  對於結果集內的每個資料行：  
  
    -   呼叫[SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)來取得結果資料行的相關資訊。  
  
     或  
  
    -   呼叫[SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)取得結果資料行的特定描述項資訊。  
  
## <a name="see-also"></a>另請參閱  
[處理結果&#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[決定結果集的特性&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
