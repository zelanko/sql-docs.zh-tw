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
ms.openlocfilehash: 816e93c7cf65d622bcd48cbf5a93eb5abba32adb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48077791"
---
# <a name="sqlcancel"></a>SQLCancel
  [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516)主題指出，在 ODBC 2.x 中，如果應用程式會呼叫`SQLCancel`陳述式上不進行任何處理時`SQLCancel`具有相同的效果`SQLFreeStmt`與`SQL_CLOSE`選項; 這只為完整性而定義行為和應用程式應該呼叫`SQLFreeStmt`或`SQLCloseCursor`來關閉資料指標。 不過，即使您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 應用程式將 ODBC API 版本設定為 3.5.x 或更新版本，`SQLCancel` 函數仍將使用 ODBC 2.x 行為。  
  
## <a name="see-also"></a>另請參閱  
 [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
