---
title: 資料行資料的長度 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- length of column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: c762c881-ebe0-4eac-84d5-f30281fc3eca
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e53cd64eaa0afb2ba042190b0649721c65979de7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="length-of-column-data"></a>資料行資料的長度
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 資料指標程式庫會建立一個緩衝區快取中，繫結至結果集，每個長度/指標緩衝區**SQLBindCol**。 它使用這些緩衝區中的值來建構**其中**子句模擬定位的 update 或 delete 陳述式時。 它會從資料來源，它會執行定位的 update 陳述式擷取資料時，它就會更新這些資料列集緩衝區的緩衝區。  
  
 如果資料緩衝區的 C 類型是 SQL_C_CHAR 或 SQL_C_BINARY，而且長度/指標值是 SQL_NTS，字串長度的資料會放入長度/指標緩衝區。  
  
> [!NOTE]  
>  如果資料指標程式庫不會更新其快取資料行 **StrLen_or_IndPtr*對應的資料列集的緩衝區是 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 巨集的結果。
