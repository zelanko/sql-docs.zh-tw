---
title: MSSQLSERVER_3151 | Microsoft Docs
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
- 3151 (Database Engine error)
ms.assetid: a8657a91-ec75-4649-a09a-21920e0030ff
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 80c5c4c20c1cadbbe4114e589c8143fec9ed828e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver3151"></a>MSSQLSERVER_3151
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|3151|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LDDB_MASTER_LOAD_FAILED|  
|訊息文字|無法還原 master 資料庫。 正在關閉 SQL Server。 Check the error logs, and rebuild the master database. 如需有關如何重建 master 資料庫的詳細資訊，請參閱《SQL Server 線上叢書》。|  
  
## <a name="explanation"></a>說明  
這是指出 **master** 資料庫發生各種問題的一般錯誤訊息。  
  
## <a name="user-action"></a>使用者動作  
檢查錯誤記錄檔以取得詳細資訊。 若要建立可以使用的 **master** 資料庫，請執行 Setup.exe，並指定 REBUILDDATABASE 選項。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜如何：從命令提示字元安裝 SQL Server＞。  
  
