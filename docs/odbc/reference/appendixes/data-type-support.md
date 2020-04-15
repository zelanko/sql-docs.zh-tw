---
title: 資料類型支援 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3abfe85ee32fb9ff4a8499c9949c0685563fec70
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284425"
---
# <a name="data-type-support"></a>資料類型支援
ODBC 驅動程式必須至少支援一個SQL_CHAR和SQL_VARCHAR。 對其他數據類型的支援由驅動程式或數據源的 SQL-92 一致性級別決定。 應用程式應呼叫**SQLGetTypeInfo**以確定驅動程式支援的數據類型。  
  
 關於資料型態的詳細資訊,請參考[資料型態的資料型態](../../../odbc/reference/appendixes/appendix-d-data-types.md)。
