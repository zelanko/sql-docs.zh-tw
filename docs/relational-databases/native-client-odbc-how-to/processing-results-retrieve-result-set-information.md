---
title: 檢索結果集資訊 (ODBC) |微軟文件
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
ms.openlocfilehash: f1c65841db0fdfd386891cfbd03bdee483ce25f6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300368"
---
# <a name="processing-results---retrieve-result-set-information"></a>處理結果 - 擷取結果集資訊
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-get-information-about-a-result-set"></a>取得結果集的相關資訊  
  
1.  呼叫[SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md)獲取結果集中的欄數。  
  
2.  對於結果集內的每個資料行：  
  
    -   致電[SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)獲取有關結果列的資訊。  
  
     Or  
  
    -   呼叫[SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)獲取有關結果列的特定描述符資訊。  
  
## <a name="see-also"></a>另請參閱  
[&#40;ODBC&#41;的流程结果](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[確定結果集的特徵&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
