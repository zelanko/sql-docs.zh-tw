---
title: MSSQLSERVER_7901 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 7901 (Database Engine error)
ms.assetid: 2d0d19b9-947b-4474-9ff8-7e03019ab93d
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cfc5c7bb78561a106130c3663c9ab11bfbf2688a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver7901"></a>MSSQLSERVER_7901
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|7901|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC2_DATABASE_IN_EMERGENCY_MODE|  
|訊息文字|未處理修復陳述式。 當資料庫處於緊急模式時不支援此修復層級。|  
  
## <a name="explanation"></a>說明  
資料庫正處於緊急模式，而且已經指定了 REPAIR_ALLOW_DATA_LOSS 以外的修復層級。 除非指定 REPAIR_ALLOW_DATA_LOSS，否則不能在緊急模式下進行修復。  
  
## <a name="user-action"></a>使用者動作  
重新執行命令，並指定 REPAIR_ALLOW_DATA_LOSS 選項。  
  
