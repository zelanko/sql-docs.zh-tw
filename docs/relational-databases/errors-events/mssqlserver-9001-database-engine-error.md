---
title: MSSQLSERVER_9001 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 228db710fffb79e9fb799d8a14125b2febe6611b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47791108"
---
# <a name="mssqlserver9001"></a>MSSQLSERVER_9001
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|9001|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LOG_NOT_AVAIL|  
|訊息文字|無法使用資料庫 '%.*ls' 的記錄檔。 相關錯誤訊息請查閱事件記錄檔。 解決任何錯誤，並重新啟動資料庫。|  
  
## <a name="explanation"></a>說明  
資料庫記錄檔已離線。 通常這種情況表示需要重新啟動資料庫的重大錯誤。  
  
## <a name="user-action"></a>使用者動作  
診斷其他錯誤並重新啟動 SQL Server 的執行個體 (如果它尚未自行重新啟動的話)。  
  
