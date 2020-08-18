---
description: MSSQLSERVER_17053
title: MSSQLSERVER_17053 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17053 (Database Engine error)
ms.assetid: e0a01f3d-d0aa-4c38-8bcc-82e59de50512
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0afb4a691519611f5b2a9e6cd5dfa365b2bbf3ce
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88334374"
---
# <a name="mssqlserver_17053"></a>MSSQLSERVER_17053
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
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
  
