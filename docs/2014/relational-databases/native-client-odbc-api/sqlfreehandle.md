---
title: SQLFreeHandle |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ba100363f3570364d9a114e8406d2b0b4c8f21f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411757"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
  在手動認可模式中，呼叫**SQLFreeHandle**陳述式上一個開啟交易的控制代碼會使暫止的變更資料庫的回復。 呼叫**SQLFreeHandle**的陳述式控制代碼永遠關閉任何開啟的資料指標並捨棄暫止的結果，請釋放陳述式控制代碼相關聯的所有資源。  
  
## <a name="see-also"></a>另請參閱  
 [SQLFreeHandle 函數](http://go.microsoft.com/fwlink/?LinkId=59345)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
