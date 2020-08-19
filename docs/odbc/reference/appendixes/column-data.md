---
description: 資料行資料
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5f4ea57de9dfefd21b6d71bb3b248d5aed5dd50d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449000"
---
# <a name="column-data"></a>資料行資料
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 資料指標程式庫會使用 **SQLBindCol**，在快取中為系結至結果集的每個資料緩衝區建立緩衝區。 它會使用這些緩衝區中的值，在模擬定位的 update 或 delete 語句時，建立 **WHERE** 子句。 當資料列集從資料來源提取資料時，以及當它執行定位的 update 語句時，它會從資料列集緩衝區更新這些緩衝區。  
  
 當資料指標程式庫從資料列集緩衝區更新其快取時，它會根據 **SQLBindCol**中指定的 C 資料類型來傳輸資料。 例如，如果 SQL_C_SLONG 資料列集緩衝區的 C 資料類型，資料指標程式庫會傳輸四個位元組的資料;如果 SQL_C_CHAR，且 *BufferLength* 為10，則資料指標程式庫會傳送10個位元組的資料。 資料指標程式庫不會對它所傳送的資料執行任何類型檢查或轉換。  
  
> [!NOTE]  
>  如果對應資料列集緩衝區中的 **StrLen_or_IndPtr* SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 宏的結果，則資料指標程式庫不會更新資料行的快取。  
  
 當它更新資料行時，資料來源會空白填補固定長度的字元資料，並視需要填補零填補的固定長度二進位資料。 例如，資料來源會將 "Smith" 儲存在 CHAR (10) 資料行做為 "Smith"。 資料指標程式庫在執行定位的 update 語句後，將資料複製到其快取時，不會在資料列集緩衝區中使用空白填充或零填補資料。 因此，如果應用程式要求資料指標程式庫快取中的值為空白填補或以零填補，則在執行定位的 update 語句之前，它必須空白或填補資料列集緩衝區中的值。
