---
title: 資料行資料 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f4bc57a5a0b500dc8828d5b0e35c2d6023165ac5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019247"
---
# <a name="column-data"></a>資料行資料
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 資料指標程式庫會在快取中，針對系結至結果集的每個資料緩衝區，使用**SQLBindCol**在快取中建立緩衝區。 當它模擬定位的 update 或 delete 語句時，它會使用這些緩衝區中的值來建立**WHERE**子句。 它會在從資料來源提取資料時，以及在執行定位 update 語句時，從資料列集緩衝區中更新這些緩衝區。  
  
 當資料指標程式庫從資料列集緩衝區更新其快取時，它會根據**SQLBindCol**中指定的 C 資料類型來傳輸資料。 例如，如果資料列集緩衝區的 C 資料類型是 SQL_C_SLONG，則資料指標程式庫會傳輸四個位元組的資料;如果 SQL_C_CHAR 且*BufferLength*為10，則資料指標程式庫會傳輸10個位元組的資料。 資料指標程式庫不會在其所傳送的資料上執行任何類型檢查或轉換。  
  
> [!NOTE]  
>  如果對應資料列集緩衝區中的 **StrLen_or_IndPtr* SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 宏的結果，則資料指標程式庫不會更新資料行的快取。  
  
 當它更新資料行時，資料來源會填補固定長度的字元資料，並視需要以零填補固定長度的二進位資料。 例如，資料來源會將 "Smith" 儲存在 CHAR （10）資料行中做為 "Smith"。 資料指標程式庫在執行定位的 update 語句之後，將此資料複製到其快取時，不會有空白 pad 或以零填補資料列集緩衝區中的資料。 因此，如果應用程式要求資料指標程式庫的快取中的值填補空白或填補零，則在執行定位的 update 語句之前，它必須以空白或零填補資料列集緩衝區中的值。
