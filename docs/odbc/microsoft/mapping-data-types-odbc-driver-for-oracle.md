---
title: 對應資料類型（ODBC Driver for Oracle） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 47646fd6fdf1e8fd16165af1bcfc5e741c6e610f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68080719"
---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>對應資料類型 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 Oracle 伺服器支援一組資料類型。 ODBC Driver for Oracle 會將這些資料類型對應到其適當的 ODBC SQL 資料類型。 下表列出 Oracle 7.3 伺服器資料類型及其對應的 ODBC SQL 資料類型。  
  
 ODBC Driver for Oracle 支援 Oracle 7.3 和一些 Oracle8 資料類型。 如需有關支援的 Oracle8 資料類型的詳細資訊，請參閱[支援的資料類型](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)。  
  
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
>  如需 VARCHAR 資料行之允許大小的詳細資訊，請參閱本指南中的[Varchar 資料行大小](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md)。
