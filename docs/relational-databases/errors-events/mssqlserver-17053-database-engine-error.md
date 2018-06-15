---
title: MSSQLSERVER_17053 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 17053 (Database Engine error)
ms.assetid: e0a01f3d-d0aa-4c38-8bcc-82e59de50512
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ea57e9570d16a3f656ef095cbf9fe6ddec175ab6
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
ms.locfileid: "34323349"
---
# <a name="mssqlserver17053"></a>MSSQLSERVER_17053
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|17053|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|OS_ERROR|  
|訊息文字|%ls: 發現作業系統錯誤 %ls。|  
  
## <a name="explanation"></a>說明  
發生一般作業系統錯誤。  不確定產生的狀態為何。  
  
## <a name="user-action"></a>使用者動作  
通常這項錯誤會與某些其他錯誤一起出現，而且應該可用來協助診斷該項失敗。 範例包括讀取或寫入失敗的資料或記錄檔、登錄讀取/寫入作業，或其他無法預期的 Win32API 失敗。  
  
