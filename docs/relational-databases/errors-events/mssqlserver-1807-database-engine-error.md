---
title: MSSQLSERVER_1807 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6042f6788352b1dae1e7922c9e3e3ba59eefb91f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver1807"></a>MSSQLSERVER_1807
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|1807|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|CANNOT_EX_LOCK|  
|訊息文字|無法取得資料庫 '%.*ls' 的獨佔鎖定。 請稍後再重試作業。|  
  
## <a name="explanation"></a>說明  
需要獨佔存取資料庫的作業無法取得適當的存取權。  
  
## <a name="user-action"></a>使用者動作  
中斷該資料庫的所有連接，或稍後再重試查詢。  
  
