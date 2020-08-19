---
description: 快取的位置
title: 快取的位置 |Microsoft Docs
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
- cache [ODBC]
ms.assetid: 240d6162-4da6-4b1f-96c7-f379f4ecb16f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 29a0c5507c1b8f581d85b0524784f8ccf1695a5f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429620"
---
# <a name="location-of-cache"></a>快取的位置
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 資料指標程式庫會將資料快取在記憶體中，而在 Windows®的暫存檔案。 這會限制資料指標程式庫只能由可用磁碟空間處理的結果集大小。 如果要快取的資料會在資料指標程式庫快取的結尾插入，則會使用暫存檔案。 相反地，會加入要快取的資料，以取代快取中最後儲存的資料區塊。 最後儲存的資料區塊會儲存在暫存檔案中。 如果資料指標程式庫異常終止，例如當電源失敗時，它可能會將 Windows 暫存檔留在磁片上。 這些名稱是 *~ CTT，* 而且是在目前的目錄中建立。  
  
> [!NOTE]  
>  如果 Microsoft® WindowsNT 中的資料指標程式庫®/Windows2000 會嘗試在應用程式從唯讀共用或精簡 (磁片執行時，在目前目錄的暫存檔案中快取資料（例如 MFC 程式庫範例) ），SQLSTATE HY000 (一般錯誤-無法建立檔案緩衝區) 將會傳回。
