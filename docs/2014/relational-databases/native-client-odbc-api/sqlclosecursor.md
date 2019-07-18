---
title: SQLCloseCursor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLCloseCursor function
ms.assetid: e7134d65-5c1c-4ae2-b119-d9b4b9a42483
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da7d6541f7bf31920519cc7462bdfd24a5f6dc0d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63067684"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
  **SQLCloseCursor**會取代[SQLFreeStmt](sqlfreestmt.md)具有*選項*SQL_CLOSE 的值。 在收到**SQLCloseCursor**，則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式會捨棄暫止的結果集資料列。 請注意，陳述式的資料行和參數繫結 （如果有的話） 會保留而不改變**SQLCloseCursor**。  
  
## <a name="see-also"></a>另請參閱  
 [SQLCloseCursor](https://go.microsoft.com/fwlink/?LinkId=59331)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
