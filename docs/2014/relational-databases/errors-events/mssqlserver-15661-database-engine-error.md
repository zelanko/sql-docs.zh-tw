---
title: MSSQLSERVER_15661 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 15661 (Database Engine error)
ms.assetid: 88b01bfb-74ce-4aa0-aec0-7885261c7ef3
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7b407f652dc2ef9bcca807c359120166d5f31f89
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022630"
---
# <a name="mssqlserver15661"></a>MSSQLSERVER_15661
    
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
  
  