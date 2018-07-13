---
title: MSSQLSERVER_2593 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 2593 (Database Engine error)
ms.assetid: 2e25bc43-606a-40de-8b87-3b55b96f4a91
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 316228d2dffa4cfcaba0bd3e6356999d4052d21a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427437"
---
# <a name="mssqlserver2593"></a>MSSQLSERVER_2593
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|2593|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_OBJECT_ROW_PAGE_SUMMARY|  
|訊息文字|物件 'OBJECT' 在 PAGECOUNT 頁面中有 ROWCOUNT 個資料列。|  
  
## <a name="explanation"></a>說明  
 這則訊息是 DBCC CHECKALLOC 以外所有 DBCC 檢查傳回之參考用輸出的一部分，而且它會指出指定之物件的資料列和頁面計數。  
  
## <a name="user-action"></a>使用者動作  
 無  
  
  
