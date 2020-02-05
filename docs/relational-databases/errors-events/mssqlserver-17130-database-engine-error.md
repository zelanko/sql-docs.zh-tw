---
title: MSSQLSERVER_17130 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17130 (Database Engine error)
ms.assetid: 7ce6afca-221d-402f-89df-da7e74a339a8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d9da9052aa4de65f93d1d2e166f1ef82df51ca62
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68076683"
---
# <a name="mssqlserver_17130"></a>MSSQLSERVER_17130
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|17130|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|INIT_NOLOCKSPACE|  
|訊息文字|記憶體不足以供已設定的鎖定數目使用。 請嘗試使用較小的鎖定雜湊表來啟動，但是可能會影響到效能。 請聯繫資料庫管理員為 Database Engine 的執行個體設定更多記憶體。|  
  
## <a name="explanation"></a>說明  
記憶體不足以供所需的鎖定管理員雜湊表大小使用。  系統將嘗試配置更小的雜湊表。  
  
## <a name="user-action"></a>使用者動作  
請檢查伺服器記憶體組態參數 (min/max server memory) 和記憶體不足的壓力。 提供 SQL Server 更多記憶體。  
  
