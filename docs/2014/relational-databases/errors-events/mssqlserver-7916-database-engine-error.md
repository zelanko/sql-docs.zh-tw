---
title: MSSQLSERVER_7916 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 7916 (Database Engine error)
ms.assetid: 9bac3536-de14-4e98-84c2-bde9a59ba0d1
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b6f885042c469bab28ed15e0e18ba39a5a94f17f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022635"
---
# <a name="mssqlserver7916"></a>MSSQLSERVER_7916
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|7916|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC2_REPAIR_RECORD_DELETED|  
|訊息文字|修復: 已刪除頁面 P_ID，位置 S_ID 上的物件識別碼 O_ID，索引識別碼 I_ID，分割區識別碼 PN_ID，配置單位識別碼 A_ID (類型 TYPE) 之記錄。 將會重建索引。|  
  
## <a name="explanation"></a>說明  
 這是來自 REPAIR 的參考用訊息，指出已經從頁面中刪除指定的記錄。  
  
## <a name="user-action"></a>使用者動作  
 無  
  
  