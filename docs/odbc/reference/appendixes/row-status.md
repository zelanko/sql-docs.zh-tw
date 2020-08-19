---
description: 資料列狀態
title: 資料列狀態 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- row status [ODBC]
- cache [ODBC]
ms.assetid: 0f0b1fb6-f697-4ced-811c-2908e210bc71
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8970e78d523ca86a50edb1e27b159ef15a1a1747
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424960"
---
# <a name="row-status"></a>資料列狀態
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 資料指標程式庫會在快取中建立資料列狀態的緩衝區。 資料指標程式庫會抓取資料列狀態陣列的值 (使用這個緩衝區) 的 SQL_ATTR_ROW_STATUS_PTR 語句屬性來指定。 針對每個資料列，資料指標程式庫會將這個緩衝區設定為：  
  
-   當它在資料列上執行定位 delete 語句時，SQL_ROW_DELETED。  
  
-   當使用 **SQLFetch**從資料來源抓取資料列時發生錯誤時，SQL_ROW_ERROR。  
  
-   當使用 **SQLFetch**成功從資料來源提取資料列時，SQL_ROW_SUCCESS。  
  
-   當它在資料列上執行定位的 update 語句時，SQL_ROW_UPDATED。
