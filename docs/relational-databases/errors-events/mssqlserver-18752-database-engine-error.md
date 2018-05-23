---
title: MSSQLSERVER_18752 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 18752 (Database Engine error)
ms.assetid: 234c58d8-7a1e-4b07-a64b-32a311527980
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c108b747a25058624bc4a66ee8ecc696d56f8309
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver18752"></a>MSSQLSERVER_18752
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
