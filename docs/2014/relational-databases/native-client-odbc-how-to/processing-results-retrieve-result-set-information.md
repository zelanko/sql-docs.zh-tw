---
title: 擷取結果集資訊 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a814a65419026dfb6e7901f2b49db2096c5da423
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409638"
---
# <a name="retrieve-result-set-information-odbc"></a>擷取結果集資訊 (ODBC)
    
### <a name="to-get-information-about-a-result-set"></a>取得結果集的相關資訊  
  
1.  呼叫[SQLNumResultCols](../native-client-odbc-api/sqlnumresultcols.md)取得結果集中的資料行數目。  
  
2.  對於結果集內的每個資料行：  
  
    -   呼叫[SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md)來取得結果資料行的相關資訊。  
  
     或  
  
    -   呼叫[SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md)取得結果資料行的特定描述項資訊。  
  
## <a name="see-also"></a>另請參閱  
 [處理結果使用說明主題&#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)   
 [決定結果集的特性&#40;ODBC&#41;](../native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
