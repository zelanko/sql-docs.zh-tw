---
title: MSSQLSERVER_5237 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 5237 (Database Engine error)
ms.assetid: 9ff28935-d1eb-47ee-99b3-1a65cb948ce7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: eabe36c423b1df3702b594137aca371a6075e327
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62867623"
---
# <a name="mssqlserver_5237"></a>MSSQLSERVER_5237
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|5237|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC4_INDEXED_VIEW_CHECK_QUERY_FAILED_NO_ERRORCODE|  
|訊息文字|物件 'NAME' (物件識別碼 O_ID) 的 DBCC 跨資料列集檢查失敗，因為發生內部查詢錯誤。|  
  
## <a name="explanation"></a>說明  
 由於發生內部錯誤，導致 DBCC 無法執行查詢來檢查索引檢視表。  
  
## <a name="user-action"></a>使用者動作  
 重新執行 DBCC 命令。  
  
  
