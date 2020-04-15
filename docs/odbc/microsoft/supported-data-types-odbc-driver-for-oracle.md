---
title: 支援的資料型態(Oracle 的 ODBC 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: 21d5f8d9-a3aa-4aa4-bc37-ff8bc90c0870
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 313254a3a117984d666d7c7be7e506386ae34e3b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301113"
---
# <a name="supported-data-types-odbc-driver-for-oracle"></a>支援的資料類型 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 Oracle 的 ODBC 驅動程式支援所有 Oracle 7.3 資料類型;但是,它不支援此處列出的任何新的 Oracle8 資料類型。  
  
|資料類型|甲骨文 7.3|甲骨文8|  
|---------------|----------------|-------------|  
|BFILE|n/a|不支援|  
|BLOB|n/a|不支援|  
|CHAR|支援|支援|  
|CLOB|n/a|不支援|  
|日期|支援|支援|  
|FLOAT|支援|支援|  
|INTEGER|支援|支援|  
|LONG|支援|支援|  
|LONG RAW|支援|支援|  
|NCHAR|n/a|不支援|  
|NCLOB|n/a|不支援|  
|NUMBER|支援|支援|  
|NVARCHAR2|n/a|不支援|  
|RAW|支援|支援|  
|VARCHAR2|支援|支援|  
|MLSLABEL|不支援。|不支援。|  
  
> [!NOTE]  
>  有關 VARCHAR 列允許大小的詳細資訊,請參閱本指南中的[VARCHAR 欄位](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md)大小 。
