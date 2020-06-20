---
title: MSSQLSERVER_3151 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3151 (Database Engine error)
ms.assetid: a8657a91-ec75-4649-a09a-21920e0030ff
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c34414754ea9d25ad89f6aba767197eb1dfc10d0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85033915"
---
# <a name="mssqlserver_3151"></a>MSSQLSERVER_3151
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|3151|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LDDB_MASTER_LOAD_FAILED|  
|訊息文字|無法還原 master 資料庫。 正在關閉 SQL Server。 Check the error logs, and rebuild the master database. 如需有關如何重建 master 資料庫的詳細資訊，請參閱《SQL Server 線上叢書》。|  
  
## <a name="explanation"></a>說明  
 這是指出 **master** 資料庫發生各種問題的一般錯誤訊息。  
  
## <a name="user-action"></a>使用者動作  
 檢查錯誤記錄檔以取得詳細資訊。 若要建立可以使用的 **master** 資料庫，請執行 Setup.exe，並指定 REBUILDDATABASE 選項。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜如何：從命令提示字元安裝 SQL Server＞。  
  
  
