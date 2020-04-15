---
title: 對應游標屬性1資訊型態 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], mapping cursor attributes1 information types
- application upgrades [ODBC], mapping cursor attributes1 information types
- mapping cursor attributes1 information types [ODBC]
- backward compatibility [ODBC], mapping cursor attributes1 information types
- upgrading applications [ODBC], mapping cursor attributes1 information types
ms.assetid: 9f112449-ca86-45ac-a865-e6174d67f91b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d70cf0a93a6c6160faeb0afe991b2adfff11b8f1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301041"
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>對應資料指標 Attributes1 資訊類型
當一個ODBC 3。*x*應用程式在 ODBC 2 *.x*驅動程式中呼叫**SQLGetInfo,** 該驅動程式具有SQL_XXXX_CURSOR_ATTRIBUTES1資訊類型(對於動態、僅轉發、鍵集驅動程式或靜態游標),驅動程式管理器返回的位元設定取決於 ODBC 2 的內容。*x*驅動程式返回相應的 ODBC 2。*x*資訊類型。 位設置為下表所示。  
  
|位元<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|資料指標類型|ODBC 2.*x*資訊<br /><br /> type|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|全部|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARK|動態鍵集驅動程式,靜態|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_UNLOCKSQL_CA1_LOCK_UNLOCKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVE|動態鍵集驅動程式,靜態|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATE|全部|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITIONSQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POS_BULK_ADD|動態鍵集驅動程式,靜態|SQL_POS_OPERATIONS|
