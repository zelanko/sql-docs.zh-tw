---
title: 快取的位置 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288616"
---
# <a name="location-of-cache"></a>快取的位置
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 游標庫在記憶體和 Windows 中快取資料®暫存檔中。 這將限制游標庫只能按可用磁碟空間處理的結果集的大小。 如果插入到游標庫緩存的末尾,則當要緩存的數據將跨越段邊界時,將使用臨時檔。 相反,要緩存的數據將添加,以代替緩存中上次保存的數據塊。 上次保存的資料塊保存在暫存檔中。 如果游標庫異常終止(例如,當電源發生故障時),它可以將 Windows 臨時檔保留在磁碟上。 這些名為 _CTT*nnnn*.tmp,並在當前目錄中創建。  
  
> [!NOTE]  
>  如果 Microsoft 中的遊標庫® WindowsNT®/Windows2000 嘗試在當前目錄中的臨時檔中緩存數據,而應用程式從唯讀共享或壓縮磁碟(如 Microsoft 基礎類庫示例)執行時,將返回 SQLSTATE HY000(無法創建檔緩衝區的一般錯誤)。
