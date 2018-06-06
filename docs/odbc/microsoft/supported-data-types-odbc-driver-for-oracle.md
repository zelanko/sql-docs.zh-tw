---
title: 支援的資料類型 （如 Oracle 的 ODBC 驅動程式） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: 21d5f8d9-a3aa-4aa4-bc37-ff8bc90c0870
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4f6e80b887659679992091a32faf2763d71d9f6f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="supported-data-types-odbc-driver-for-oracle"></a>支援的資料類型 （如 Oracle 的 ODBC 驅動程式）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 Oracle 的 ODBC 驅動程式支援所有 Oracle 7.3 資料型別。不過，它不支援任何此處所列的新 Oracle8 資料型別。  
  
|資料類型|Oracle 7.3|Oracle8|  
|---------------|----------------|-------------|  
|BFILE|n/a|不支援|  
|BLOB|n/a|不支援|  
|CHAR|Supported|Supported|  
|CLOB|n/a|不支援|  
|DATE|Supported|Supported|  
|FLOAT|Supported|Supported|  
|INTEGER|Supported|Supported|  
|LONG|Supported|Supported|  
|LONG RAW|Supported|Supported|  
|NCHAR|n/a|不支援|  
|NCLOB|n/a|不支援|  
|NUMBER|Supported|Supported|  
|NVARCHAR2|n/a|不支援|  
|RAW|Supported|Supported|  
|VARCHAR2|Supported|Supported|  
|MLSLABEL|不支援。|不支援。|  
  
> [!NOTE]  
>  VARCHAR 資料行的允許大小的相關資訊，請參閱[VARCHAR 資料行大小](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md)本指南中。
