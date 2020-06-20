---
title: MSSQLSERVER_17128 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17128 (Database Engine error)
ms.assetid: 7b15a5e6-fd41-47ce-ba87-54f72acea4bb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0e08c668acd0a8b2decb14da338b8d1f1e650de5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967887"
---
# <a name="mssqlserver_17128"></a>MSSQLSERVER_17128
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|17128|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|INIT_NOBUFSPACE|  
|訊息文字|initdata: 未提供記憶體給核心緩衝區。|  
  
## <a name="explanation"></a>說明  
 緩衝集區的初始記憶體配置或保留已經失敗，而且 SQL Server 結束。  
  
## <a name="user-action"></a>使用者動作  
 通常是由於在非常小型的電腦 (遠低於最低系統需求) 上啟動 SQL Server 所造成。  
  
  
