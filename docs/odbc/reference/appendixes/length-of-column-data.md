---
title: 資料行資料長度 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- length of column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: c762c881-ebe0-4eac-84d5-f30281fc3eca
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8d2998eace4772624a1e6590ab2541577147f5c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041615"
---
# <a name="length-of-column-data"></a>資料行資料長度
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 資料指標程式庫會繫結至結果集，每個長度/指標緩衝區快取中建立一個緩衝區**SQLBindCol**。 它使用這些緩衝區中的值來建構**其中**子句模擬定位的 update 或 delete 陳述式時。 它會從資料來源，以及當它執行定位的 update 陳述式的擷取資料時，它就會更新這些資料列集的緩衝區的緩衝區。  
  
 如果將資料緩衝區的 C 類型為 SQL_C_CHAR 或 SQL_C_BINARY，長度/指標值為 SQL_NTS，則會將字串長度的資料放入長度/指標緩衝區。  
  
> [!NOTE]  
>  資料指標程式庫不會更新其快取的資料行，如果 **StrLen_or_IndPtr*中對應的資料列集的緩衝區是 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 巨集的結果。
