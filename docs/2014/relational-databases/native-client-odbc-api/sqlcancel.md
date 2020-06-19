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
author: rothja
ms.author: jroth
ms.openlocfilehash: dc3d86229501f80b25fb077788d1835a5f4f5c96
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022899"
---
# <a name="sqlcancel"></a>SQLCancel
  [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)主題指出，在 ODBC 2.x 中，如果應用程式在 `SQLCancel` 未于語句上進行處理時呼叫，其效果與 `SQLCancel` `SQLFreeStmt` 選項相同 `SQL_CLOSE` ; 此行為只會針對完整性而定義，而應用程式應該呼叫 `SQLFreeStmt` 或 `SQLCloseCursor` 來關閉資料指標。 不過，即使您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 應用程式將 ODBC API 版本設定為 3.5.x 或更新版本，`SQLCancel` 函數仍將使用 ODBC 2.x 行為。  
  
## <a name="see-also"></a>另請參閱  
 [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
