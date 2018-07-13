---
title: MSSQLSERVER_8689 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 8689 (Database Engine error)
ms.assetid: 99467a32-6576-4272-a076-b16c06933f2a
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 85e33cc4231fb4ebf6a3058a20a0257e81a07b6a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37421437"
---
# <a name="mssqlserver8689"></a>MSSQLSERVER_8689
    
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
 [查詢提示 &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [計畫指南](../performance/plan-guides.md)  
  
  
