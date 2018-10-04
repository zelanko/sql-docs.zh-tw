---
title: SQLFreeHandle |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b5a7e09a6dd9bbcc50ddbaf70b911260e96cde4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48214677"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
  在手動認可模式中，呼叫**SQLFreeHandle**陳述式上一個開啟交易的控制代碼會使暫止的變更資料庫的回復。 呼叫**SQLFreeHandle**的陳述式控制代碼永遠關閉任何開啟的資料指標並捨棄暫止的結果，請釋放陳述式控制代碼相關聯的所有資源。  
  
## <a name="see-also"></a>另請參閱  
 [SQLFreeHandle 函數](http://go.microsoft.com/fwlink/?LinkId=59345)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
