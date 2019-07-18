---
title: MSSQLSERVER_12329 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 12329 (Database Engine error)
ms.assetid: 43f90287-36d5-46c2-ac91-a37202dcf6d3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a8eb921f8993b4ad689f266b6d9c45c9d7d42720
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62859966"
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
  
