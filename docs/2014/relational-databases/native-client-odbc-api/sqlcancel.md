---
title: SQLCancel |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8bad2cc35a30f5c6f5855292ff73635cef6072b2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63067835"
---
# <a name="sqlcancel"></a>SQLCancel
  [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)主題指出，在 ODBC 2.x 中，如果應用程式在語句上`SQLCancel`未進行任何處理時呼叫， `SQLCancel`與`SQLFreeStmt` `SQL_CLOSE`選項的效果相同。此行為僅針對完整性而定義，而應用程式`SQLFreeStmt`應該`SQLCloseCursor`呼叫或來關閉資料指標。 不過，即使您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 應用程式將 ODBC API 版本設定為 3.5.x 或更新版本，`SQLCancel` 函數仍將使用 ODBC 2.x 行為。  
  
## <a name="see-also"></a>另請參閱  
 [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
