---
title: MSSQLSERVER_7915 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 7915 (Database Engine error)
ms.assetid: 63338587-7dd3-40e6-b70e-d8ae18fff47b
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fd2358d9fda87cfe7f1d25dc45ef475606165eb4
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver7915"></a>MSSQLSERVER_7915
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|7915|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC2_REPAIR_IAM_CHAIN_REBUILT|  
|訊息文字|修復: 物件識別碼 O_ID，索引識別碼 I_ID，分割區識別碼 PN_ID，配置單位識別碼 A_ID (類型 TYPE) 的 IAM 鏈已在頁面 P_ID 之前截斷，將會重建。|  
  
## <a name="explanation"></a>說明  
這是由 REPAIR 傳送的參考用資訊，指出已經修補指定的索引配置對應 (IAM) 鏈結，因此可以重建該鏈結。 這項修補動作可能已經要求配置 IAM 鏈結的新標頭，或是從鏈結中移除錯誤的頁面。  
  
## <a name="user-action"></a>使用者動作  
無  
  

