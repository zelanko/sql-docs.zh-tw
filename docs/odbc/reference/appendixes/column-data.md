---
title: 資料行的資料 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019247"
---
# <a name="column-data"></a>資料行資料
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 資料指標程式庫會繫結至結果集，每個資料緩衝區快取中建立一個緩衝區**SQLBindCol**。 它使用這些緩衝區中的值來建構**其中**子句時，它會模擬定位的 update 或 delete 陳述式。 它會從資料來源，以及當它執行定位的 update 陳述式的擷取資料時，它就會更新這些資料列集的緩衝區的緩衝區。  
  
 當資料指標程式庫更新其快取，從資料列集的緩衝區時，它會將資料傳輸根據中指定的 C 資料類型**SQLBindCol**。 例如，如果 SQL_C_SLONG C 資料類型的資料列集的緩衝區，資料指標程式庫傳送四個位元組的資料;如果是 SQL_C_CHAR 並*Columnsize*為 10，資料指標程式庫傳輸資料的 10 個位元組。 資料指標程式庫不會執行任何類型檢查或轉換它所傳輸的資料。  
  
> [!NOTE]  
>  資料指標程式庫不會更新其快取的資料行，如果 **StrLen_or_IndPtr*中對應的資料列集的緩衝區是 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 巨集的結果。  
  
 當更新資料行、 資料來源空白填補固定長度的字元資料和視需要零填補固定長度二進位資料。 例如，資料來源會儲存"Smith"CHAR(10) 資料行中為"Smith"。 會將此資料複製到其快取上執行定位的 update 陳述式之後不空白填補或零填補的資料列集的緩衝區中的資料來執行並資料指標程式庫。 因此，如果應用程式需要在資料指標程式庫的快取中的值是空白填補或填補零，則它必須空白填補或零填補的資料列集的緩衝區中的值執行定位的 update 陳述式之前。
