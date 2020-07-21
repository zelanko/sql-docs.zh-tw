---
title: MSSQLSERVER_17053 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17053 (Database Engine error)
ms.assetid: e0a01f3d-d0aa-4c38-8bcc-82e59de50512
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e7ddd06b7a49cb0b7d1495e0960248c0aa6564d2
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553733"
---
# <a name="mssqlserver_17053"></a>MSSQLSERVER_17053
    
## <a name="details"></a>詳細資料  
  
|屬性|值|  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|17053|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|OS_ERROR|  
|訊息文字|%ls:發現作業系統錯誤 %ls。|  
  
## <a name="explanation"></a>說明  
 發生一般作業系統錯誤。  不確定產生的狀態為何。  
  
## <a name="user-action"></a>使用者動作  
 通常這項錯誤會與某些其他錯誤一起出現，而且應該可用來協助診斷該項失敗。 範例包括讀取或寫入失敗的資料或記錄檔、登錄讀取/寫入作業，或其他無法預期的 Win32API 失敗。  
  
  
