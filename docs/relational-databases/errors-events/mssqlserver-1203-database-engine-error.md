---
title: MSSQLSERVER_1203 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 1203 (Database Engine error)
ms.assetid: 33a35f00-98c8-46c6-b432-544b326b6117
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9c283411d8b2508a931a8fb66873e37985ae86cd
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver1203"></a>MSSQLSERVER_1203
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|1203|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LK_NOT|  
|訊息文字|處理序識別碼 %d 嘗試解除鎖定不是它所擁有的資源: %.*ls。 請重試交易，因為這種錯誤可能是時間狀況造成的。 如果問題仍然存在，請連絡資料庫管理員。|  
  
## <a name="explanation"></a>說明  
當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在執行一些不同於平常後置處理清除的活動，並且發現它嘗試要解除鎖定的特定頁面已經解除鎖定時，就會發生這個錯誤。  
  
### <a name="possible-causes"></a>可能的原因  
造成這個錯誤的根本原因，可能與受影響的資料庫內部的結構問題有關。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會管理頁面的鎖定與解除鎖定，以維護多使用者環境中的並行控制。 這個機制是透過使用各種不同可識別目前頁面及鎖定類型的內部鎖定來維護。 處理受影響的頁面時會進行鎖定，處理完成之後便會解除鎖定。  
  
## <a name="user-action"></a>使用者動作  
針對物件所屬的資料庫執行 DBCC CHECKDB。 如果 DBCC CHECKDB 回報沒有錯誤，請嘗試重新建立連接並執行命令。  
  
> [!IMPORTANT]  
> 如果執行包含其中一個 REPAIR 子句的 DBCC CHECKDB 後無法更正問題，或者您不確定包含 REPAIR 子句的 DBCC CHECKDB 對資料有何效果，請與主要支援提供者連絡。  
  
