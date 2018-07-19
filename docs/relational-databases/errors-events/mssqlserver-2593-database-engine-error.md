---
title: MSSQLSERVER_2593 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 2593 (Database Engine error)
ms.assetid: 2e25bc43-606a-40de-8b87-3b55b96f4a91
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bb1c4cef6aa746a7d8db78d7d5c46db699207c8a
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
ms.locfileid: "34319069"
---
# <a name="mssqlserver2593"></a>MSSQLSERVER_2593
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
