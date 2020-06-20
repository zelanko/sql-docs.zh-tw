---
title: MSSQLSERVER_3413 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3413 (Database Engine error)
ms.assetid: 3fa07637-ba93-4633-aaf2-ade7d18bc487
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a5d59ea61cff7051c3e1163a463c29443c553923
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85033530"
---
# <a name="mssqlserver_3413"></a>MSSQLSERVER_3413
    
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
  
  
