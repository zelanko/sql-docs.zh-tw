---
title: MSSQLSERVER_17803 | Microsoft Docs
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
- 17803 (Database Engine error)
ms.assetid: 28591a19-258d-4891-b78a-4686789bb2d7
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a96b9970406ee7da627ac955e1fe280a12b7f90e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver17803"></a>MSSQLSERVER_17803
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|17803|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SRV_NOMEMORY|  
|訊息文字|建立連接期間發生記憶體配置錯誤。 請減少非必要的記憶體載入，或增加系統記憶體。 此連接已經關閉。%.*ls|  
  
## <a name="explanation"></a>說明  
伺服器記憶體不足。  
  
## <a name="user-action"></a>使用者動作  
判斷伺服器記憶體不足的原因。 一般記憶體疑難排解步驟可能會很有用。  
  
