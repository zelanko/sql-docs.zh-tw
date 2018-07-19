---
title: 使用自動擷取搭配 ODBC 資料指標 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, autofetch
- autofetch option
- cursors [ODBC], autofetch
ms.assetid: 57bd55f4-8945-4d8d-9f58-d30c81d2a514
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc376d6ecc536ce95c8b2ffdd60d972211b271f8
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417347"
---
# <a name="using-autofetch-with-odbc-cursors"></a>使用自動擷取搭配 ODBC 資料指標
  當連接到的執行個體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，則[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式時使用任何伺服器資料指標類型，支援自動擷取選項。 使用自動擷取時， **SQLExecute**或是**SQLExecDirect**開啟資料指標的函式也具有隱含[SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md)(SQL_FIRST) 函數。 構成第一個資料列集的資料列會當做陳述式執行的一部分而傳回至繫結的應用程式變數，如此就不需要再一次透過網路往返伺服器。 [SQLGetData](../../native-client-odbc-api/sqlgetdata.md)時不支援已啟用自動擷取選項; 將結果集資料行必須繫結至程式變數。  
  
 應用程式會藉由將驅動程式特定的 SQL_SOPT_SS_CURSOR_OPTIONS 陳述式屬性設定為 SQL_CO_AF 來要求自動擷取。  
  
## <a name="see-also"></a>另請參閱  
 [資料指標程式設計詳細資料&#40;ODBC&#41;](cursor-programming-details-odbc.md)  
  
  
