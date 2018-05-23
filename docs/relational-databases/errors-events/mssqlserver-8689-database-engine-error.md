---
title: MSSQLSERVER_8689 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 8689 (Database Engine error)
ms.assetid: 99467a32-6576-4272-a076-b16c06933f2a
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2011d72a8d58e6c3c21f8fe746eb8c5b901ccb8d
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver8689"></a>MSSQLSERVER_8689
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|8689|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|USEPLAN_ERR_NO_DB|  
|訊息文字|USE PLAN 提示中指定的資料庫 '%.*ls' 不存在。 請指定現有的資料庫。|  
  
## <a name="explanation"></a>說明  
在 USE PLAN 提示中指定的資料庫不存在。  
  
## <a name="user-action"></a>使用者動作  
請確定在 USE PLAN 提示中指定的所有資料庫都存在。  
  
## <a name="see-also"></a>另請參閱  
[查詢提示 &#40;Transact-SQL&#41;](~/t-sql/queries/hints-transact-sql-query.md)  
[計畫指南](~/relational-databases/performance/plan-guides.md)  
  
