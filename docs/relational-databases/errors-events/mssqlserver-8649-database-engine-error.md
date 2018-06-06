---
title: MSSQLSERVER_8649 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 8649 (Database Engine error)
ms.assetid: 992dbc74-7c3a-498b-9f1b-b28387640677
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: edba4ff99095e796db323d9588d2963070d24805
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver8649"></a>MSSQLSERVER_8649
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|8649|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|COST_TOO_HIGH|  
|訊息文字|查詢已經取消，因為這個查詢 (%d) 的預估成本超過了設定的臨界值 %d。 請連絡系統管理員。|  
  
## <a name="explanation"></a>說明  
由於查詢的預估成本超過了 QUERY_GOVERNOR_COST_LIMIT 設定的臨界值，因此已經取消查詢。  
  
## <a name="user-action"></a>使用者動作  
將 QUERY_GOVERNOR_COST_LIMIT 選項設定成較高的值。  
  
## <a name="see-also"></a>另請參閱  
[SET QUERY_GOVERNOR_COST_LIMIT &#40;Transact-SQL&#41;](~/t-sql/statements/set-query-governor-cost-limit-transact-sql.md)  
  
