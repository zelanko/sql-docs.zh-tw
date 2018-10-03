---
title: MSSQLSERVER_17130 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17130 (Database Engine error)
ms.assetid: 7ce6afca-221d-402f-89df-da7e74a339a8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4f8d62a98d39a65db78f79fdfaf3ecdb2921408e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48142871"
---
# <a name="mssqlserver17130"></a>MSSQLSERVER_17130
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|17130|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|INIT_NOLOCKSPACE|  
|訊息文字|記憶體不足以供已設定的鎖定數目使用。 請嘗試使用較小的鎖定雜湊表來啟動，但是可能會影響到效能。 請聯繫資料庫管理員為 Database Engine 的執行個體設定更多記憶體。|  
  
## <a name="explanation"></a>說明  
 記憶體不足以供所需的鎖定管理員雜湊表大小使用。  系統將嘗試配置更小的雜湊表。  
  
## <a name="user-action"></a>使用者動作  
 請檢查伺服器記憶體組態參數 (min/max server memory) 和記憶體不足的壓力。 提供 SQL Server 更多記憶體。  
  
  
