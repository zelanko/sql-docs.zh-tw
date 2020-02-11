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
ms.openlocfilehash: 21495e538a554a477336d1a92926c11fe762c5af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68062657"
---
# <a name="checking-feature-support-and-variability"></a>檢查功能支援和變化性
若要檢查功能支援和變化性，應用程式通常會呼叫**SQLGetInfo**、 **SQLGetFunctions**和**SQLGetTypeInfo**。 驅動程式的 API 和 SQL 文法一致性層級是很好的起點。 這些描述廣泛的功能支援層級。 然後，應用程式可以使用其他選項來呼叫**SQLGetInfo** ，以判斷其所需的功能支援或變化性， **SQLGetFunctions**以判斷所需的函式超出傳回的一致性層級，並**SQLGetTypeInfo**判斷支援哪些 SQL 資料類型。  
  
 應用程式可以藉由呼叫**SQLSetStmtAttr**或**SQLSetConnectAttr**與該屬性，來判斷語句或連接屬性是否受到支援。 如果函數傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，則支援屬性;如果它傳回 SQL_ERROR 並 SQLSTATE HYC00 （未實作為選擇性功能），則不支援此屬性。  
  
 應用程式也可以藉由呼叫**SQLDrivers**，在連接到驅動程式之前判斷有限的資訊數量。
