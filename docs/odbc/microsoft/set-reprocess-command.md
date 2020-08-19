---
description: SET REPROCESS 命令
title: 設定重新處理命令 |Microsoft Docs
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
ms.openlocfilehash: 8daeebd38f295d437dc02c1c34126c30f6426b68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421822"
---
# <a name="set-reprocess-command"></a>SET REPROCESS 命令
指定在失敗的鎖定嘗試之後，鎖定檔案或記錄的時間長度。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>引數  
 至 *nAttempts*[秒]  
 指定嘗試在初始失敗嘗試後鎖定記錄或檔案的次數或秒數。 預設值為 0;最大值為32000。  
  
 SECONDS 指定 Visual FoxPro 嘗試鎖定檔案或記錄的 *nAttempts* 秒數。 只有當 *nAttempts* 大於零時，才能使用此功能。  
  
 例如，如果 *nAttempts* 為30，則 Visual FoxPro 會嘗試鎖定記錄或檔案，最多30次。 如果您也包含秒鐘 (將重新處理設定為30秒) ，Visual FoxPro 會持續嘗試鎖定記錄或檔案，最多30秒。  
  
 如果 ON ERROR 常式有效，且如果命令嘗試鎖定記錄或檔案失敗，則會執行 ON ERROR 常式。 但是，如果函式嘗試鎖定，就不會執行 ON ERROR 常式，且函數會傳回 False (。F. ) 。  
  
 如果錯誤常式不在作用中，命令會嘗試鎖定記錄或檔案，而且無法放置鎖定，就會產生錯誤。 如果函式嘗試放置鎖定，就不會顯示警示，而且函數會傳回 False (。F. ) 。  
  
 如果 *nAttempts* 為 0 (預設值) 而且您發出嘗試鎖定記錄或檔案的命令或函數，則 Visual FoxPro 會嘗試無限期地鎖定記錄或檔案。 如果記錄檔或檔案在等候時變成可供鎖定，就會放置鎖定，並清除系統訊息。 如果函式嘗試放置鎖定，函數會傳回 True (。) 。  
  
 如果 ON ERROR 常式作用中，且某個命令嘗試鎖定記錄或檔案，則 ON ERROR 常式優先于鎖定記錄或檔案的其他嘗試。 ON ERROR 常式會立即執行。 Visual FoxPro 不會嘗試其他記錄或檔案鎖定，也不會顯示系統訊息。  
  
 如果 *nAttempts* 是1，則 Visual FoxPro 會嘗試無限期地鎖定記錄或檔案，而且不會執行 ON ERROR 常式。  
  
 如果另一位使用者在您嘗試鎖定的記錄或檔案上放置鎖定，您必須等到使用者釋放鎖定為止。  
  
 自動  
 指定 Visual FoxPro 嘗試無限期地鎖定記錄或檔案。  (SET 重新處理為-2 是對等的命令。 )   
  
## <a name="remarks"></a>備註  
 第一次嘗試鎖定記錄或檔案時，不一定會成功。 通常會由網路上的另一位使用者鎖定記錄或檔案。 SET 重新處理可判斷在初始嘗試失敗時，Visual FoxPro 是否會額外嘗試鎖定記錄或檔案。 您可以指定要進行多少次額外的嘗試，或進行嘗試的時間長度。 ON ERROR 常式會影響處理失敗鎖定嘗試的方式。
