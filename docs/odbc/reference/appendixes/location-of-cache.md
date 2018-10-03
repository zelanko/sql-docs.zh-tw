---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b1ffd8c56a6727a892cb518222c961bbb6c794c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649086"
---
# <a name="location-of-cache"></a>快取的位置
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 資料指標程式庫會快取在記憶體中和 Windows® 暫存檔案的資料。 這會限制結果集資料指標程式庫可處理只受可用磁碟空間的大小。 快取資料會跨越區段界限，如果資料指標程式庫快取的結尾插入時，會使用暫存檔案。 相反地，取代最後儲存的資料區塊快取中加入快取的資料。 上次儲存的資料區塊會儲存在暫存檔中。 如果資料指標程式庫終止異常，例如當電源失敗時，它可以讓 Windows 在磁碟上的暫存檔案。 這些都命名為 ~ CTT*nnnn*.tmp 並建立在目前的目錄。  
  
> [!NOTE]  
>  如果資料指標程式庫中 Microsoft® WindowsNT®/Windows2000 嘗試在目前的目錄上的暫存檔案中的快取資料的唯讀共用或光碟 （例如 Microsoft Foundation 類別程式庫範例），從執行應用程式時 SQLSTATEHY000 （一般錯誤-無法建立檔案緩衝區） 會傳回。
