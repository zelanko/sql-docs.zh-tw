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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9345a02d446d8a4b7b82e9652444a08f68641f87
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706074"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
  在手動認可模式中，使用開啟的交易在語句控制碼上呼叫**SQLFreeHandle** ，會導致資料庫的暫止變更回復。 在語句控制碼上呼叫**SQLFreeHandle**一律會關閉任何開啟的資料指標，並捨棄暫止的結果，釋放與語句控制碼相關聯的所有資源。  
  
## <a name="see-also"></a>另請參閱  
 [SQLFreeHandle 函式](https://go.microsoft.com/fwlink/?LinkId=59345)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
