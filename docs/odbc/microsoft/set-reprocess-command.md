---
title: 設定重新處理命令 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET REPROCESS command [ODBC]
ms.assetid: b0708757-b1d7-42f3-8988-787f2a806b8b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5a7eb5fd19ca538c4f25077926567011ae133e54
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300828"
---
# <a name="set-reprocess-command"></a>SET REPROCESS 命令
指定鎖定鎖定失敗後鎖定檔案或記錄的次數或時間。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>引數  
 到*n 次嘗試*[秒]  
 指定在初始嘗試失敗後嘗試鎖定記錄或檔案的次數或秒數。 默認值為 0;最大值為 32,000。  
  
 SECONDS 指定 Visual FoxPro 嘗試鎖定檔或記錄,但時間*為 n,時間*數秒。 僅當*n 次次次次*大於零時,它才可用。  
  
 例如,如果*nATos*為 30,Visual FoxPro 會嘗試鎖定記錄或檔最多 30 次。 如果您還包括 SECONDS(SET REPROCESS 到 30 秒),Visual FoxPro 會不斷嘗試鎖定記錄或檔長達 30 秒。  
  
 如果 ON ERROR 例程有效,並且命令鎖定記錄或檔的嘗試不成功,則執行 ON ERROR 例程。 但是,如果函數嘗試鎖定,則不會執行 ON ERROR 例程,並且函數返回 False ()。F.)。  
  
 如果 ON ERROR 例程無效,命令將嘗試鎖定記錄或檔,並且無法放置鎖,則產生錯誤。 如果函數嘗試放置鎖,則不顯示警報,並且函數返回 False ()。F.)。  
  
 如果*nTries*為 0(預設值),並且您發出一個命令或函數,嘗試鎖定記錄或檔,Visual FoxPro 將嘗試無限期鎖定記錄或檔。 如果等待時記錄或檔可用於鎖定,則鎖定並清除系統消息。 如果函數嘗試放置鎖,則函數返回 True (。T.)。  
  
 如果 ON ERROR 例程有效,並且命令嘗試鎖定記錄或檔,則 ON ERROR 例程優先於鎖定記錄或檔的其他嘗試。 立即執行 ON ERROR 例程。 Visual FoxPro 不會嘗試其他記錄或檔鎖,也不會顯示系統消息。  
  
 如果*nATos*為 1,Visual FoxPro 會嘗試無限期鎖定記錄或檔,並且不會執行 ON ERROR 例程。  
  
 如果其他使用者已在您嘗試鎖定的記錄或檔中放置了鎖,則必須等待使用者釋放鎖。  
  
 到自動  
 指定 Visual FoxPro 嘗試無限期鎖定記錄或檔。 (將 REPROCESS 設置為 -2 是等效命令。  
  
## <a name="remarks"></a>備註  
 首次嘗試鎖定記錄或檔並不總是成功的。 通常,記錄或檔被網路上的其他用戶鎖定。 SET REPROCESS 確定 Visual FoxPro 在初始嘗試不成功時是否進行了其他嘗試來鎖定記錄或檔。 您可以指定進行額外嘗試的次數或嘗試的時間。 ON ERROR 例程會影響處理不成功的鎖嘗試的方式。
