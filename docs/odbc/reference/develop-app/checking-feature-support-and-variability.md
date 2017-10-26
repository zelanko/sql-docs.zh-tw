---
title: "檢查功能的支援和變化 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: ff45f220-9b8b-4c44-82f8-a8e9913fffea
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5528f451adf12d12fe5cdb1c51f5c5d0053c9145
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="checking-feature-support-and-variability"></a>檢查功能的支援和變化
若要檢查功能的支援和變化，應用程式通常會呼叫**SQLGetInfo**， **SQLGetFunctions**，和**SQLGetTypeInfo**。 好的起點是驅動程式的 API 和 SQL 文法一致性層級。 其中說明功能支援廣泛的層的級。 應用程式可以接著呼叫**SQLGetInfo**與其他選項來判斷其所需的功能的變化性的支援**SQLGetFunctions**來判斷是否超過傳回需要函數支援的一致性層級，以及**SQLGetTypeInfo**以判斷支援哪些 SQL 資料型別。  
  
 應用程式就可以判斷是否支援陳述式或連接屬性呼叫**SQLSetStmtAttr**或**SQLSetConnectAttr**具有該屬性。 如果函數傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，被支援的屬性。如果它會傳回 SQL_ERROR 並 SQLSTATE HYC00 （選擇性功能未實作），不支援的屬性。  
  
 應用程式也可以決定將有限的數量的資訊，才能連接到驅動程式，藉由呼叫**SQLDrivers**。

