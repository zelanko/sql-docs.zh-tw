---
title: MSSQLSERVER_15661 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 15661 (Database Engine error)
ms.assetid: 88b01bfb-74ce-4aa0-aec0-7885261c7ef3
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 93bd2efde15065f2d7285912a72a10a7ba77d817
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver15661"></a>MSSQLSERVER_15661
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|15661|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum15661|  
|訊息文字|sp_estimate_data_compression_savings 預存程序無法用於暫存資料表。|  
  
## <a name="explanation"></a>說明  
暫存資料表當做 sp_estimate_data_compression_savings 預存程序的引數使用。 雖然暫存資料表的壓縮有受到支援，但是您無法使用 sp_estimate_data_compression_savings 來預估所節省的壓縮。  
  
## <a name="user-action"></a>使用者動作  
移除當做 sp_estimate_data_compression_savings 之引數的暫存資料表。  
  

