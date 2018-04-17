---
title: SET 重新處理命令 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SET REPROCESS command [ODBC]
ms.assetid: b0708757-b1d7-42f3-8988-787f2a806b8b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fb1ee7ee957ef5a7872a87a47d5615f1d241aa6b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="set-reprocess-command"></a>SET 重新處理命令
指定多少次，或如何的長度，鎖定的嘗試失敗後鎖定檔案或記錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>引數  
 若要*nAttempts*[秒]  
 指定的次數或嘗試鎖定記錄或檔案失敗的初始嘗試之後的秒數。 預設值是 0;最大值是 32000。  
  
 秒數指定 Visual FoxPro 嘗試鎖定的檔案或記錄*nAttempts*秒。 它是只有*nAttempts*大於零。  
  
 例如，如果*nAttempts*為 30，Visual FoxPro 會嘗試鎖定記錄或檔案高達 30 倍。 如果您也會包含秒 （設定重新處理至 30 秒為單位），Visual FoxPro 會持續嘗試鎖定最多 30 秒的記錄或檔案。  
  
 如果 ON 錯誤常式作用中，如果鎖定記錄或檔案的命令的嘗試不成功，則會執行 ON 錯誤常式。 不過，如果函式會嘗試鎖定，ON 錯誤常式未執行，此函數會傳回 False (。F.)。  
  
 如果 ON 錯誤常式不是作用中，命令會嘗試鎖定記錄或檔案，且無法鎖定，會產生錯誤。 如果函式所要放置鎖定，不會顯示警示，而且函數會傳回 False (。F.)。  
  
 如果*nAttempts*是 0 （預設值），而且您發出的命令或嘗試鎖定記錄或檔案的函式，Visual FoxPro 嘗試鎖定記錄或無限期檔案。 如果記錄或檔案會變成可用於鎖定等候期間，會放置鎖定，並清除系統訊息。 如果函式試圖放置鎖定，函數會傳回 True (。T)。  
  
 如果 ON 錯誤常式作用中，命令會嘗試鎖定記錄或檔案，ON 錯誤常式優先於其他嘗試来鎖定的記錄或檔案。 ON 錯誤常式便會立即執行。 Visual FoxPro 不會嘗試其他的記錄或檔案鎖定，並不會顯示系統訊息。  
  
 如果*nAttempts*為 1、 Visual FoxPro 嘗試鎖定記錄或無限期檔案和 ON 錯誤常式未執行。  
  
 如果已將鎖定放另一位使用者的記錄或您嘗試要鎖定的檔案，您必須等到使用者釋放鎖定。  
  
 為自動  
 指定 Visual FoxPro 嘗試鎖定記錄或無限期檔案。 （-2 組重新處理是對應的命令）。  
  
## <a name="remarks"></a>備註  
 第一次嘗試鎖定記錄或檔案不一定會成功。 經常的記錄或檔案已在網路上的另一位使用者被鎖定。 設定重新處理決定 Visual FoxPro 是否會鎖定記錄或檔案的初始嘗試失敗時的其他嘗試。 您可以指定其他嘗試進行，或進行多久嘗試多少次。 ON 錯誤常式會影響如何成功處理嘗試的鎖定。
