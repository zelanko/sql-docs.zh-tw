---
title: MSSQLSERVER_2593 | Microsoft Docs
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
- 2593 (Database Engine error)
ms.assetid: 2e25bc43-606a-40de-8b87-3b55b96f4a91
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 09d12991e0e440f9be3ef8ba37da6decc94aa47d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133494"
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
  
  