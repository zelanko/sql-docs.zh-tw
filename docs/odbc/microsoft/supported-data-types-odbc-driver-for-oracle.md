---
title: "支援的資料類型 （如 Oracle 的 ODBC 驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: 21d5f8d9-a3aa-4aa4-bc37-ff8bc90c0870
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7ea00ac6b2e95b2bd21453312a42ef2769b20d9c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="supported-data-types-odbc-driver-for-oracle"></a>支援的資料類型 （如 Oracle 的 ODBC 驅動程式）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 Oracle 的 ODBC 驅動程式支援所有 Oracle 7.3 資料型別。不過，它不支援任何此處所列的新 Oracle8 資料型別。  
  
|資料類型|Oracle 7.3|Oracle8|  
|---------------|----------------|-------------|  
|BFILE|n/a|不支援|  
|BLOB|n/a|不支援|  
|CHAR|支援|支援|  
|CLOB|n/a|不支援|  
|DATE|支援|支援|  
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
>  VARCHAR 資料行的允許大小的相關資訊，請參閱[VARCHAR 資料行大小](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md)本指南中。
