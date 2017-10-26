---
title: MSSQLSERVER_4064 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 4064 (Database Engine error)
ms.assetid: 32112b90-0a2f-4834-a027-756811732be7
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ff8f948a1c94fcfcb36f43d0644e251e027a02c5
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver4064"></a>MSSQLSERVER_4064
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|4064|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DB_UFAIL_FATAL|  
|訊息文字|無法開啟使用者預設資料庫。 登入失敗。|  
  
## <a name="explanation"></a>說明  
由於預設資料庫發生問題，SQL Server 登入無法連接。 可能是資料庫本身無效，或是登入在資料庫上沒有 CONNECT 權限。  
  
## <a name="user-action"></a>使用者動作  
使用 ALTER LOGIN 變更登入的預設資料庫。 授與 CONNECT 權限給登入。  
  

