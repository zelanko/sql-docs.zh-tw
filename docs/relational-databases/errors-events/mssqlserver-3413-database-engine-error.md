---
description: MSSQLSERVER_3413
title: MSSQLSERVER_3413 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3413 (Database Engine error)
ms.assetid: 3fa07637-ba93-4633-aaf2-ade7d18bc487
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f031909aa618376cf3ed347c1bfd0fcd1beff307
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88332174"
---
# <a name="mssqlserver_3413"></a>MSSQLSERVER_3413
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|3413|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|MARKDB|  
|訊息文字|資料庫識別碼 %d。 無法將資料庫標示為有疑問。 sys.databases.database_id 上的 Getnext NC 掃描失敗。 請參閱錯誤記錄檔中之前的錯誤，以找出原因，並修正所有相關問題。|  
  
## <a name="explanation"></a>說明  
嘗試在目錄中將使用者資料庫標示為 SUSPECT 時發生非預期的錯誤。 SUSPECT 狀態不會保存下來。  
  
## <a name="user-action"></a>使用者動作  
參閱先前的錯誤並更正問題。  
  
