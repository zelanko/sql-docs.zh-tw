---
description: 資料行資料長度
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
ms.openlocfilehash: 96194272d6b291da53986330199d9c7972cef8f1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429660"
---
# <a name="length-of-column-data"></a>資料行資料長度
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 資料指標程式庫會使用 **SQLBindCol**，在快取中為系結至結果集的每個長度/指標緩衝區建立緩衝區。 它會使用這些緩衝區中的值，在它模擬定位的 update 或 delete 語句時，建立 **WHERE** 子句。 當資料列集從資料來源提取資料時，以及當它執行定位的 update 語句時，它會從資料列集緩衝區更新這些緩衝區。  
  
 如果資料緩衝區的 C 類型是 SQL_C_CHAR 或 SQL_C_BINARY，而且長度/指標值 SQL_NTS，則資料的字串長度會放入長度/指標緩衝區中。  
  
> [!NOTE]  
>  如果對應資料列集緩衝區中的 **StrLen_or_IndPtr* SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 宏的結果，則資料指標程式庫不會更新資料行的快取。
