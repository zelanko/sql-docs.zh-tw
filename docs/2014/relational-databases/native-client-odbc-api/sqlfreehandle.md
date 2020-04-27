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
ms.openlocfilehash: 197d3e1d36f8513821cec9630cade8f52681a43d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63154668"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
  在手動認可模式中，使用開啟的交易在語句控制碼上呼叫**SQLFreeHandle** ，會導致資料庫的暫止變更回復。 在語句控制碼上呼叫**SQLFreeHandle**一律會關閉任何開啟的資料指標，並捨棄暫止的結果，釋放與語句控制碼相關聯的所有資源。  
  
## <a name="see-also"></a>另請參閱  
 [SQLFreeHandle 函式](https://go.microsoft.com/fwlink/?LinkId=59345)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
