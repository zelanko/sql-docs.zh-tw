---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16f87c52b4149d62a8d57884216890b7421e8ef6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063626"
---
# <a name="set-reprocess-command"></a>SET REPROCESS 命令
指定在失敗的鎖定嘗試之後，鎖定檔案或記錄的次數或時間長度。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>引數  
 TO *nAttempts*[SECONDS]  
 指定嘗試在初始嘗試失敗後鎖定記錄或檔案的次數或秒數。 預設值為 0;最大值為32000。  
  
 SECONDS 指定 Visual FoxPro 會嘗試鎖定檔案或記錄以達*nAttempts*秒數。 只有當*nAttempts*大於零時，才可以使用它。  
  
 例如，如果*nAttempts*為30，Visual FoxPro 會嘗試鎖定記錄或檔案，最多30次。 如果您也包含秒（將重新處理設定為30秒），Visual FoxPro 會持續嘗試鎖定一或多個記錄或檔案長達30秒。  
  
 如果 ON ERROR 常式作用中，而且如果命令嘗試鎖定記錄或檔案失敗，則會執行 ON ERROR 常式。 不過，如果函式嘗試鎖定，則不會執行 ON ERROR 常式，而且函數會傳回 False （。F.）。  
  
 如果 ON ERROR 常式沒有作用，命令會嘗試鎖定記錄或檔案，而且無法放置鎖定，就會產生錯誤。 如果函式嘗試放置鎖定，則不會顯示警示，而且函數會傳回 False （。F.）。  
  
 如果*nAttempts*為0（預設值），而您發出嘗試鎖定記錄或檔案的命令或函式，Visual FoxPro 會嘗試無限期地鎖定記錄或檔案。 如果記錄檔或檔案在您等候時變成可供鎖定，則會放置鎖定並清除系統訊息。 如果函數嘗試放置鎖定，此函式會傳回 True （。T.）。  
  
 如果「發生錯誤」常式生效，而命令嘗試鎖定記錄或檔案，則「錯誤」常式的優先順序會高於其他鎖定記錄或檔案的嘗試。 ON ERROR 常式會立即執行。 Visual FoxPro 不會嘗試其他記錄或檔案鎖定，也不會顯示系統訊息。  
  
 如果*nAttempts*是1，Visual FoxPro 會嘗試無限期地鎖定記錄或檔案，而且不會執行 ON ERROR 常式。  
  
 如果另一位使用者在您嘗試鎖定的記錄或檔案上放置鎖定，您必須等到使用者釋放鎖定。  
  
 自動  
 指定 Visual FoxPro 嘗試無限期地鎖定記錄或檔案。 （將重新處理設定為-2 是對等的命令）。  
  
## <a name="remarks"></a>備註  
 第一次嘗試鎖定記錄或檔案不一定都會成功。 通常，記錄或檔案是由網路上的另一個使用者鎖定。 設定重新處理決定 Visual FoxPro 是否會在初始嘗試失敗時，額外嘗試鎖定記錄或檔案。 您可以指定進行其他嘗試的次數，或進行嘗試的時間長度。 ON ERROR 常式會影響失敗的鎖定嘗試處理方式。
