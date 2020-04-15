---
title: 映射資料類型(Oracle 的 ODBC 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping data types [ODBC]
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: a5d9ce12-19da-4943-8493-e3d56fa08348
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 432c21b70efcdd63ef36bfe3d26f8488ddb11d1d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302669"
---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>對應資料類型 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 Oracle 伺服器支援一組數據類型。 Oracle 的 ODBC 驅動程式將這些資料類型映射到其適當的 ODBC SQL 資料類型。 下表列出了 Oracle 7.3 伺服器數據類型及其相應的 ODBC SQL 資料類型。  
  
 Oracle 的 ODBC 驅動程式支援 Oracle 7.3 和某些 Oracle 8 資料類型。 有關受支援的 Oracle8 資料類型的詳細資訊,請參閱[受支援的資料類型](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)。  
  
|Oracle 伺服器資料類型|ODBC SQL 資料類型|  
|-----------------------------|------------------------|  
|CHAR|SQL_CHAR|  
|日期|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_DECIMAL|  
|LONG|SQL_LONGVARCHAR|  
|LONG RAW|SQL_LONGVARBINARY|  
|NUMBER|SQL_DECIMAL|  
|RAW|SQL_VARBINARY|  
|VARCHAR2|SQL_VARCHAR|  
  
> [!NOTE]  
>  有關 VARCHAR 列允許大小的詳細資訊,請參閱本指南中的[VARCHAR 欄位](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md)大小 。
