---
title: 取出結果集資訊（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3017f74b12eb18624f8a34e8a1289da18b70c93a
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82712700"
---
# <a name="retrieve-result-set-information-odbc"></a>擷取結果集資訊 (ODBC)
    
### <a name="to-get-information-about-a-result-set"></a>取得結果集的相關資訊  
  
1.  呼叫[SQLNumResultCols](../native-client-odbc-api/sqlnumresultcols.md)以取得結果集內的資料行數目。  
  
2.  對於結果集內的每個資料行：  
  
    -   呼叫[SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md)以取得結果資料行的相關資訊。  
  
     或  
  
    -   呼叫[SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md)以取得結果資料行的特定描述元資訊。  
  
## <a name="see-also"></a>另請參閱  
 [處理結果如何 &#40;ODBC&#41;的 how to 主題](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)   
 [判斷結果集的特性 &#40;ODBC&#41;](../native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
