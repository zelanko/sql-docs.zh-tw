---
title: MSSQLSERVER_17887 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17887 (Database Engine error)
ms.assetid: ad0806e6-3296-4c32-b103-fccf0f8a8d3d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 006e616d80ef7e8d083f60675b02b4e6a4e8dc24
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967748"
---
# <a name="mssqlserver_17887"></a>MSSQLSERVER_17887
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|17887|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SRV_IO_COMP_LISTENER_NONYIELDING|  
|訊息文字|IO Completion Listener (0x%lx) 工作者 0x%p 在節點 %ld 上似乎沒有產量。 已使用的約略 CPU: 核心 %I64d ms，使用者 %I64d ms，間隔: %I64d。|  
  
## <a name="explanation"></a>說明  
 表示針對網路讀取/寫入事件執行 I/O 完成常式時，指定之節點上的 I/O 完成通訊埠 (Completion Port) 接聽程式可能發生問題。 當 I/O 完成通訊埠接聽程式從執行 I/O 完成常式返回時，這個錯誤就會消失。  
  
## <a name="user-action"></a>使用者動作  
 請連絡 Microsoft 客戶支援服務 (CSS)。  
  
  
