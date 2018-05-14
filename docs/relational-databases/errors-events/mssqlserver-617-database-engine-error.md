---
title: MSSQLSERVER_617 | Microsoft Docs
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
- 617 (Database Engine error)
ms.assetid: 213545d9-08a7-4427-bfd1-8b7e16644281
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b908e9f8702716b6bb5626845ea9b1c2be714ac8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver617"></a>MSSQLSERVER_617
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|617|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|NODESHASH|  
|訊息文字|嘗試取消資料庫識別碼 %d 中物件識別碼 %ld 的雜湊時，在雜湊表中找不到該描述項。 工作資料表遺漏一個項目。 請重新執行查詢。 如果資料指標與此有關，請先關閉，然後重新開啟資料指標。|  
  
## <a name="explanation"></a>說明  
SQL Server 找不到特定項目的工作資料表。  
  
## <a name="user-action"></a>使用者動作  
  
1.  如果資料指標與此有關，請先關閉資料指標，然後重新開啟資料指標。  
  
2.  再次執行查詢。  
  
