---
title: 檢查功能支援和可變性 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47f16160c05d1c410e3889f0bb857befe88df5b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299168"
---
# <a name="checking-feature-support-and-variability"></a>檢查功能支援和變化性
為了檢查功能支援與可變性,應用程式通常呼叫**SQLGetInfo、SQLGet****函數**與**SQLGetTypeInfo**。 一個好的起始位置是驅動程式的 API 和 SQL 語法符合性級別。 這些描述了廣泛的功能支援級別。 然後,應用程式可以調用**SQLGetInfo**與其他選項一起確定其需要的功能的支援或可變性 **,SQLGet 函數**確定是否支援超出返回的一致性級別所需的功能,以及**SQLGetTypeInfo**來確定支援哪些 SQL 資料類型。  
  
 應用程式可以通過使用該屬性調用**SQLSetStmtAttr**或**SQLSetConnectAttr**來確定敘述或連接屬性是否受支援。 如果函數返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,則屬性受支援;如果函數返回該屬性,則為該屬性。如果它返回SQL_ERROR和 SQLSTATE HYC00(未實現可選功能),則不支援該屬性。  
  
 應用程式還可以通過調用**SQLDriver**在連接到驅動程式之前確定有限的資訊量。
