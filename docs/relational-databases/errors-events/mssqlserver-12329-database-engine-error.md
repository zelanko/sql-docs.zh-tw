---
title: MSSQLSERVER_12329 | Microsoft Docs
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
- 12329 (Database Engine error)
ms.assetid: 43f90287-36d5-46c2-ac91-a37202dcf6d3
caps.latest.revision: 4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 559e0daaea2271a78d21a0e38f41ce130b278ce4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver12329"></a>MSSQLSERVER_12329
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|12329|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|HK_UNSUPPORTED_NON_LATIN_CODEPAGE|  
|訊息文字|*construct* 不支援資料類型 char(n) 和 varchar(n) 使用包含非 1252 之字碼頁的定序。|  
  
## <a name="explanation"></a>說明  
如有資料類型 char(n) 和 varchar(n) 使用包含非 1252 之字碼頁的定序，請勿使用這些資料類型。  
  
## <a name="user-action"></a>使用者動作  
其中一個會產生此錯誤的非預期的狀況為：  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = 'us_english')  
```  
  
請改用：  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
```  
  
