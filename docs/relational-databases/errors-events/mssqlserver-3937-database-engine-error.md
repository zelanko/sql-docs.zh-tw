---
title: MSSQLSERVER_3937 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8f40def8cedfcdd2a090941fb2dc8a6547a2d766
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3937"></a>MSSQLSERVER_3937
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|MSSQLSERVER|  
|事件識別碼|3937|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|XACT_FILESTREAM_ROLLBACK_ERROR|  
|訊息文字|嘗試通知檔案資料流篩選驅動程式已回復交易時發生錯誤。 錯誤碼: 0x%0x。|  
  
## <a name="explanation"></a>說明  
當發出交易的回復通知時，RsFx 驅動程式傳回了錯誤。 這可能是因為資源短缺所造成。 這會造成 RsFx 篩選驅動程式內的小型記憶體遺漏，但是當建立交易的 sqlservr.exe 處理序結束時，將會釋出這些記憶體。  
  
## <a name="user-action"></a>使用者動作  

