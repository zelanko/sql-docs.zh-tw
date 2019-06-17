---
title: MSSQLSERVER_617 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 617 (Database Engine error)
ms.assetid: 213545d9-08a7-4427-bfd1-8b7e16644281
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f63983243d0859fcb7ebaaf1ac5d184757d1f274
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62867198"
---
# <a name="mssqlserver617"></a>MSSQLSERVER_617
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|617|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|NODESHASH|  
|訊息文字|嘗試取消資料庫識別碼 %d 中物件識別碼 %ld 的雜湊時，在雜湊表中找不到該描述項。 工作資料表遺漏一個項目。 請重新執行查詢。 如果資料指標與此有關，請先關閉，然後重新開啟資料指標。|  
  
## <a name="explanation"></a>說明  
 SQL Server 找不到特定項目的工作資料表。  
  
## <a name="user-action"></a>使用者動作  
  
1.  如果資料指標與此有關，請先關閉資料指標，然後重新開啟資料指標。  
  
2.  再次執行查詢。  
  
  
