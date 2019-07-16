---
title: SET REPROCESS 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16f87c52b4149d62a8d57884216890b7421e8ef6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063626"
---
# <a name="set-reprocess-command"></a>SET REPROCESS 命令
指定多少時間，或如何鎖定的嘗試失敗後的檔案或記錄長時間。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>引數  
 若要*nAttempts*[秒]  
 指定的次數或嘗試失敗的初始嘗試之後鎖定記錄或檔案的秒數。 預設值是 0;最大值是 32000。  
  
 秒數可讓您指定 Visual FoxPro 嘗試鎖定的檔案或記錄*nAttempts*秒。 它是時才可使用*nAttempts*是小於或等於零。  
  
 例如，如果*nAttempts*為 30、 Visual FoxPro 嘗試鎖定記錄或檔案最多 30 倍。 如果您也會包含秒 （設定重新處理到 30 秒），Visual FoxPro 會持續嘗試鎖定記錄或檔案，最多 30 秒。  
  
 如果 ON ERROR 」 常式處於作用中和鎖定記錄或檔案的命令的嘗試未成功，則會執行 ON ERROR 常式。 不過，如果函式會嘗試鎖定，ON ERROR 」 常式不會執行，則函數會傳回 False (。F.) 中。  
  
 如果 ON ERROR 」 常式沒有作用，命令會嘗試鎖定記錄或檔案，而且無法在鎖定，則會產生錯誤。 如果函式會嘗試讓鎖定，不會顯示警示，則函數會傳回 False (。F.) 中。  
  
 如果*nAttempts*為 0 （預設值） 和您發出的命令或嘗試鎖定記錄或檔案的函式、 Visual FoxPro 嘗試鎖定記錄，或無限期地檔案。 如果記錄或檔案會變成可用於鎖定在等候時，會放置鎖定，並清除系統訊息。 如果函式會嘗試放置鎖定，此函數會傳回 True (。T)。  
  
 如果 ON ERROR 」 常式處於作用中，命令會嘗試鎖定記錄或檔案的 ON ERROR 」 常式優先於其他嘗試鎖定記錄或檔案。 ON ERROR 常式便會立即執行。 Visual FoxPro 不會嘗試其他記錄或檔案鎖定，並不會顯示系統訊息。  
  
 如果*nAttempts*為 1、 Visual FoxPro 嘗試鎖定記錄，或無限期地檔案和 ON ERROR 」 常式不會執行。  
  
 如果鎖定已放在記錄或您正嘗試將鎖定的檔案上的另一位使用者，您必須等到使用者解除鎖定。  
  
 為自動  
 指定 Visual FoxPro 嘗試鎖定記錄，或無限期地檔案。 （設定為-2 的重新處理是對等的命令）。  
  
## <a name="remarks"></a>備註  
 第一次嘗試鎖定記錄或檔案不一定會成功。 通常，記錄或檔案已在網路上的另一位使用者被鎖定。 設定重新處理，以判斷是否 Visual FoxPro 可讓其他嘗試鎖定記錄或檔案，當初始嘗試失敗時。 您可以指定額外的嘗試進行，或進行多久嘗試次數。 ON ERROR 」 常式會影響如何成功處理嘗試的鎖定。
