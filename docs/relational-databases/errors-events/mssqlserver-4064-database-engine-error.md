---
title: MSSQLSERVER_4064 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 4064 (Database Engine error)
ms.assetid: 32112b90-0a2f-4834-a027-756811732be7
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c58d5a054999da21c3b2850e529a067df0edfb22
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
ms.locfileid: "34318759"
---
# <a name="mssqlserver4064"></a>MSSQLSERVER_4064
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|4064|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DB_UFAIL_FATAL|  
|訊息文字|無法開啟使用者預設資料庫。 登入失敗。|  
  
## <a name="explanation"></a>說明  
由於預設資料庫發生問題，SQL Server 登入無法連接。 可能是資料庫本身無效，或是登入在資料庫上沒有 CONNECT 權限。  
  
## <a name="user-action"></a>使用者動作  
使用 ALTER LOGIN 變更登入的預設資料庫。 授與 CONNECT 權限給登入。  
  
