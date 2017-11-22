---
title: MSSQLSERVER_12329 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 12329 (Database Engine error)
ms.assetid: 43f90287-36d5-46c2-ac91-a37202dcf6d3
caps.latest.revision: "4"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 09cec5db6647fe03aa21d019c8546a2aea5cbb5f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver12329"></a>MSSQLSERVER_12329
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
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
  
