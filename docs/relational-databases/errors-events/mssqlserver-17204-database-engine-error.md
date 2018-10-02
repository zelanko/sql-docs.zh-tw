---
title: MSSQLSERVER_17204 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: 40db66f9-dd5e-478c-891e-a06d363a2552
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d8bfda451cda9b27670abc180ded16ceca7d7cab
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680006"
---
# <a name="mssqlserver17204"></a>MSSQLSERVER_17204
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|17204|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBLKIO_DEVOPENFAILED|  
|訊息文字|%ls: 無法開啟檔案 %ls，檔案編號為 %d。  作業系統錯誤: %ls。|  
  
## <a name="explanation"></a>說明  
SQL Server 無法開啟指定的檔案，因為發生指定的錯誤。  
  
## <a name="user-action"></a>使用者動作  
診斷並更正作業系統，然後重試此作業。  
  
