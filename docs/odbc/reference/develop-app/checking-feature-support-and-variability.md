---
title: 檢查功能支援和變化性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: ff45f220-9b8b-4c44-82f8-a8e9913fffea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b9af2cfd73556baca4870428cdcdfcee3e07191d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63217614"
---
# <a name="checking-feature-support-and-variability"></a>檢查功能支援和變化性
若要檢查功能的支援和變化，應用程式通常會呼叫**SQLGetInfo**， **SQLGetFunctions**，並**SQLGetTypeInfo**。 好的起點是驅動程式的 API 和 SQL 文法一致性層級。 其中說明所支援之功能的廣泛程度。 應用程式接著可以呼叫**SQLGetInfo**來判斷所支援或變化性的功能，其所需的其他選項**SQLGetFunctions**來判斷是否超過傳回需要函數支援的一致性層級，以及**SQLGetTypeInfo**來判斷支援哪些 SQL 資料類型。  
  
 應用程式可以藉由呼叫是否支援陳述式或連接屬性來判斷**SQLSetStmtAttr**或是**SQLSetConnectAttr**具有該屬性。 如果函數傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，被支援的屬性;如果它傳回 SQL_ERROR，而且 SQLSTATE HYC00 （未實作選擇性功能），不支援的屬性。  
  
 應用程式也可以判斷數量有限的資訊，然後再連接到驅動程式，藉由呼叫**SQLDrivers**。
