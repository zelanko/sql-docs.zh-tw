---
description: MSSQLSERVER_3151
title: MSSQLSERVER_3151 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3151 (Database Engine error)
ms.assetid: a8657a91-ec75-4649-a09a-21920e0030ff
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4d787407483cfe29c02fe48fa985cfa024dfdfed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491196"
---
# <a name="mssqlserver_3151"></a>MSSQLSERVER_3151
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|3151|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LDDB_MASTER_LOAD_FAILED|  
|訊息文字|無法還原 master 資料庫。 正在關閉 SQL Server。 請檢查錯誤記錄檔並重建 master 資料庫。 如需有關如何重建 master 資料庫的詳細資訊，請參閱《SQL Server 線上叢書》。|  
  
## <a name="explanation"></a>說明  
這是指出 **master** 資料庫發生各種問題的一般錯誤訊息。  
  
## <a name="user-action"></a>使用者動作  
檢查錯誤記錄檔以取得詳細資訊。 若要建立可以使用的 **master** 資料庫，請執行 Setup.exe，並指定 REBUILDDATABASE 選項。 如需詳細資訊，請參閱＜如何：從命令提示字元安裝 SQL Server＞(位於《SQL Server 線上叢書》中)。  
  
