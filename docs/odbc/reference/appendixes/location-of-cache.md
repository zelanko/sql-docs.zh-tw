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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 13510332ae8bfab07a13d7831f9f74a048551214
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288616"
---
# <a name="location-of-cache"></a>快取的位置
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 游標程式庫會將資料快取到記憶體中，而在 Windows®的暫存檔案中。 這會限制資料指標程式庫只能透過可用磁碟空間處理的結果集大小。 當要快取的資料在資料指標程式庫快取的結尾插入時，會使用暫存檔案。 相反地，會加入要快取的資料，以取代快取中最後儲存的資料區塊。 最後儲存的資料區塊會儲存在暫存檔案中。 如果資料指標程式庫異常終止（例如當電源失敗時），它可能會將 Windows 暫存檔案留在磁片上。 這些名稱會命名為 ~ CTT*nnnn*.tmp，並在目前的目錄中建立。  
  
> [!NOTE]  
>  如果 Microsoft® WindowsNT 中的資料指標程式庫®會在應用程式從唯讀共用或光碟（例如 MFC 程式庫範例）中執行時，嘗試快取目前目錄的暫存檔案中的資料，則會傳回 SQLSTATE HY000 （一般錯誤-無法建立檔案緩衝區）。
