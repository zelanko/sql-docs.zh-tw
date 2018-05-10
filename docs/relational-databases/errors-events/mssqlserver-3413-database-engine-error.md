---
title: MSSQLSERVER_3413 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 3413 (Database Engine error)
ms.assetid: 3fa07637-ba93-4633-aaf2-ade7d18bc487
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9cfa7a7f5b40767776c0db4ac58918ccf45080f4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver3413"></a>MSSQLSERVER_3413
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|3413|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|MARKDB|  
|訊息文字|資料庫識別碼 %d。 無法將資料庫標示為有疑問。 sys.databases.database_id 上的 Getnext NC 掃描失敗。 請參閱錯誤記錄檔中之前的錯誤，以找出原因，並修正所有相關問題。|  
  
## <a name="explanation"></a>說明  
嘗試在目錄中將使用者資料庫標示為 SUSPECT 時發生非預期的錯誤。 SUSPECT 狀態不會保存下來。  
  
## <a name="user-action"></a>使用者動作  
參閱先前的錯誤並更正問題。  
  
