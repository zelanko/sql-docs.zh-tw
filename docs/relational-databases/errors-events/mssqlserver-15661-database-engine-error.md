---
title: MSSQLSERVER_15661 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 15661 (Database Engine error)
ms.assetid: 88b01bfb-74ce-4aa0-aec0-7885261c7ef3
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 089727123d4edc9ed5f1e30e4e9cd187b5ee0bbf
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver15661"></a>MSSQLSERVER_15661
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|15661|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum15661|  
|訊息文字|sp_estimate_data_compression_savings 預存程序無法用於暫存資料表。|  
  
## <a name="explanation"></a>說明  
暫存資料表當做 sp_estimate_data_compression_savings 預存程序的引數使用。 雖然暫存資料表的壓縮有受到支援，但是您無法使用 sp_estimate_data_compression_savings 來預估所節省的壓縮。  
  
## <a name="user-action"></a>使用者動作  
移除當做 sp_estimate_data_compression_savings 之引數的暫存資料表。  
  
