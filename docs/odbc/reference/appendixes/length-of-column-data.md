---
title: 欄資料的長度 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d0b7ad515661cce4c5b1d407be768cc3da131bb4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304929"
---
# <a name="length-of-column-data"></a>資料行資料長度
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 游標庫在緩存中為每個長度/指示器緩衝區創建一個緩衝區,該緩衝區綁定到使用**SQLBindCol**綁定到結果集。 當它們類比定位的更新或刪除語句時,它使用這些緩衝區中的值來構造**WHERE**子句。 當從數據源獲取數據並執行定位更新語句時,它會從行集緩衝區更新這些緩衝區。  
  
 如果數據緩衝區的 C 類型SQL_C_CHAR或SQL_C_BINARY,並且長度 / 指示器值SQL_NTS,則數據的字串長度將放入長度 / 指示器緩衝區中。  
  
> [!NOTE]  
>  如果相應的行集*緩衝區中的*StrLen_or_IndPtrSQL_DATA_AT_EXEC或SQL_LEN_DATA_AT_EXEC宏的結果,則游標庫不會更新列的緩存。
