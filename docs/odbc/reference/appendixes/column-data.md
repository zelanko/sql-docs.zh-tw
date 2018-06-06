---
title: 資料行資料 |Microsoft 文件
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
- column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 0425818c-9469-493f-9e3c-fc03d9411c5c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 428f7c4a9d0e21cb989721b095b65bf0c48306fe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="column-data"></a>資料行資料
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 資料指標程式庫建立快取中，繫結至結果集，每個資料緩衝區的緩衝區**SQLBindCol**。 它使用這些緩衝區中的值來建構**其中**子句時，它會模擬定位的 update 或 delete 陳述式。 它會從資料來源，它會執行定位的 update 陳述式擷取資料時，它就會更新這些資料列集緩衝區的緩衝區。  
  
 當資料指標程式庫更新其快取中的資料列集的緩衝區時，它會將資料傳輸中指定的 C 資料類型根據**SQLBindCol**。 舉例來說，如果資料列集緩衝區的 C 資料類型是 SQL_C_SLONG，資料指標程式庫傳送四個位元組的資料;如果是 SQL_C_CHAR 和*Columnsize*為 10，資料指標程式庫傳輸資料的 10 個位元組。 資料指標程式庫不會執行任何類型檢查或轉換的資料傳輸。  
  
> [!NOTE]  
>  如果資料指標程式庫不會更新其快取資料行 **StrLen_or_IndPtr*對應的資料列集的緩衝區是 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 巨集的結果。  
  
 當更新資料行、 資料來源空白填補的固定長度的字元資料和零填補視固定長度二進位資料。 例如，資料來源會儲存"Smith"char （10） 資料行中為"Smith"。 資料指標程式庫時它將此資料複製到快取上執行定位的 update 陳述式之後，請執行未填補的空白或零填補的資料列集的緩衝區中的資料。 因此，如果應用程式需要的資料指標程式庫的快取中的值空白填補或填補零，則它必須空白填補或零填補的資料列集的緩衝區中的值執行定位的 update 陳述式之前。
