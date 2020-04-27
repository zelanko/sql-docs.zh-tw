---
title: 資料行資料的長度 |Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304929"
---
# <a name="length-of-column-data"></a>資料行資料長度
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 資料指標程式庫會在快取中，針對系結至結果集的每個長度/指標緩衝區，使用**SQLBindCol**在快取中建立緩衝區。 它會在模擬定位 update 或 delete 語句時，使用這些緩衝區中的值來建立**WHERE**子句。 它會在從資料來源提取資料時，以及在執行定位 update 語句時，從資料列集緩衝區中更新這些緩衝區。  
  
 如果資料緩衝區的 C 類型是 SQL_C_CHAR 或 SQL_C_BINARY，而且長度/指標值 SQL_NTS，則資料的字串長度會放入長度/指標緩衝區中。  
  
> [!NOTE]  
>  如果對應資料列集緩衝區中的 **StrLen_or_IndPtr* SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 宏的結果，則資料指標程式庫不會更新資料行的快取。
