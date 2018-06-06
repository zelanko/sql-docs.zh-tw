---
title: MSSQLSERVER_1807 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e7cdba5b23f82f7051966ca171abaf18fed8e0d0
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver1807"></a>MSSQLSERVER_1807
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|1807|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|CANNOT_EX_LOCK|  
|訊息文字|無法取得資料庫 '%.*ls' 的獨佔鎖定。 請稍後再重試作業。|  
  
## <a name="explanation"></a>說明  
需要獨佔存取資料庫的作業無法取得適當的存取權。  
  
## <a name="user-action"></a>使用者動作  
中斷該資料庫的所有連接，或稍後再重試查詢。  
  
