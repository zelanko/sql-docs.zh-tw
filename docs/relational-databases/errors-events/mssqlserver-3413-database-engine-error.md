---
title: MSSQLSERVER_3413 | Microsoft Docs
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
- 3413 (Database Engine error)
ms.assetid: 3fa07637-ba93-4633-aaf2-ade7d18bc487
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 38900b11bc5e2892ea85f22db2a6c1490d6399fb
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3413"></a>MSSQLSERVER_3413
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|3413|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|MARKDB|  
|訊息文字|資料庫識別碼 %d。 無法將資料庫標示為有疑問。 sys.databases.database_id 上的 Getnext NC 掃描失敗。 請參閱錯誤記錄檔中之前的錯誤，以找出原因，並修正所有相關問題。|  
  
## <a name="explanation"></a>說明  
嘗試在目錄中將使用者資料庫標示為 SUSPECT 時發生非預期的錯誤。 SUSPECT 狀態不會保存下來。  
  
## <a name="user-action"></a>使用者動作  
參閱先前的錯誤並更正問題。  
  

