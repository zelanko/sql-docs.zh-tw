---
title: MSSQLSERVER_17128 | Microsoft Docs
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
- 17128 (Database Engine error)
ms.assetid: 7b15a5e6-fd41-47ce-ba87-54f72acea4bb
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f4cb960b5da644f114fee64ead0e122915000ba9
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver17128"></a>MSSQLSERVER_17128
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|17128|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|INIT_NOBUFSPACE|  
|訊息文字|initdata: 未提供記憶體給核心緩衝區。|  
  
## <a name="explanation"></a>說明  
緩衝集區的初始記憶體配置或保留已經失敗，而且 SQL Server 結束。  
  
## <a name="user-action"></a>使用者動作  
通常是由於在非常小型的電腦 (遠低於最低系統需求) 上啟動 SQL Server 所造成。  
  

