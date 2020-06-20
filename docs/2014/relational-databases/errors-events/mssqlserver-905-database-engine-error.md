---
title: MSSQLSERVER_905 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 905 (Database Engine error)
ms.assetid: c828bb2e-e554-4f81-b76c-2b3740d2b944
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7dd3c8c5a287e2d123e2a9d1430ecd49b27f29f5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85031529"
---
# <a name="mssqlserver_905"></a>MSSQLSERVER_905
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|905|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBSTARTUP_EE_PARTITIONING|  
|訊息文字|資料庫 '%.*ls' 無法在此版本的 SQL Server 中啟動，因為它包含資料分割函式 '%.\*ls'。 只有 Enterprise Edition 的 SQL Server 才支援分割區。|  
  
## <a name="explanation"></a>說明  
 資料庫包含一個或多個分割的資料表或索引。 這一版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法使用資料分割。 因此，資料庫無法正確啟動。 並非每個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本都可使用資料分割資料表和索引。 如需版本支援的功能清單 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請參閱[SQL Server 2014 版本支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="user-action"></a>使用者動作  
 使用 sp_detach_db 預存程序來卸離資料庫。 視需要移動檔案，然後將資料庫附加到所支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的執行個體，其方式是搭配 FOR ATTACH 或 FOR ATTACH_REBUILD_LOG 選項使用 CREATE DATABASE。 停用所有資料表上的資料分割，並移除資料分割函數。 再次卸離資料庫，然後將資料庫重新附加到目前的伺服器。  
  
  
