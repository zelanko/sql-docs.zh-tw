---
title: MSSQLSERVER_1807 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 69acb74bd1c50900ae4852c41b3304da7ca7c00c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48092223"
---
# <a name="mssqlserver1807"></a>MSSQLSERVER_1807
    
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
  
  
