---
title: 欄數據 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 0425818c-9469-493f-9e3c-fc03d9411c5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ff89566efa65c88325d98422fe17788f27d2c8ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306589"
---
# <a name="column-data"></a>資料行資料
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 游標庫在緩存中為每個使用**SQLBindCol**綁定到結果集的數據緩衝區創建一個緩衝區。 當它們類比定位的更新或刪除語句時,它使用這些緩衝區中的值來構造**WHERE**子句。 當從數據源獲取數據並執行定位更新語句時,它會從行集緩衝區更新這些緩衝區。  
  
 當游標庫從行集緩衝區更新其緩存時,它會根據**SQLBindCol**中指定的 C 數據類型傳輸數據。 例如,如果排集緩衝區的 C 數據類型SQL_C_SLONG,則游標庫傳輸四個字節的數據;如果游標庫傳輸四個字節的數據。如果它是SQL_C_CHAR緩衝區*長度*為 10,則游標庫傳輸 10 位元組的數據。 游標庫不對傳輸的數據執行任何類型檢查或轉換。  
  
> [!NOTE]  
>  如果相應的行集*緩衝區中的*StrLen_or_IndPtrSQL_DATA_AT_EXEC或SQL_LEN_DATA_AT_EXEC宏的結果,則游標庫不會更新列的緩存。  
  
 更新列時,數據源空白板固定長度字元數據和零墊固定長度二進位數據將根據需要進行。 例如,資料源將 CHAR (10) 列中的「Smith」儲存為「Smith」。。 游標庫在執行定位的更新語句后將此數據複製到其緩存時,不會在行集緩衝區中出現空白板或零板數據。 因此,如果應用程式要求游標庫緩存中的值為空白填充值或零填充值,則必須在執行定位的更新語句之前對行集緩衝區中的值進行空白填充或零填充。
