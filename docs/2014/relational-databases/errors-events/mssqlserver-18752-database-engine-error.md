---
title: MSSQLSERVER_18752 | Microsoft Docs
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
- 18752 (Database Engine error)
ms.assetid: 234c58d8-7a1e-4b07-a64b-32a311527980
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e37d24643f2c095e9b2ed15061f9b96952c5be9f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136859"
---
# <a name="mssqlserver18752"></a>MSSQLSERVER_18752
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|18752|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|REPL_INUSE|  
|訊息文字|一次只有一個記錄讀取器代理程式或記錄檔相關程序 (sp_repldone, sp_replcmds, and sp_replshowcmds) 可連接到資料庫。 若您已執行記錄檔相關程序，請卸除執行程序的連接，或者利用該連接執行 sp_replflush 之後，再啟動記錄讀取器代理程式或執行其他記錄檔相關程序。|  
  
## <a name="explanation"></a>說明  
 每次只有一個記錄讀取器代理程式或記錄檔相關程序可以連接到資料庫。  
  
## <a name="user-action"></a>使用者動作  
 確定沒有其他記錄讀取器正在針對相同的發行資料庫執行，而且沒有其他使用中的連接先前已經執行 sp_replcmds/sp_repltrans/sp_repldone 而事後沒有執行 sp_replflush 或中斷連接。  
  
  