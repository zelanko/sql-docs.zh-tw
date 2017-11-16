---
title: "設定平行處理原則的最大程度選項來取得最佳效能 | Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6efd8d390f0f468b8e4236190e58d52acc043a62
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>設定平行處理原則的最大程度選項來取得最佳效能
  此規則會判斷某個值的 max degree of parallelism (MAXDOP) 選項是否大於 8。 將這個選項設定為較大的值通常會造成不必要的資源耗用，而且會降低效能。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 使用 sp_configure 將 max degree of parallelism 選項設定為 8。  
  
## <a name="for-more-information"></a>詳細資訊  
 [Microsoft 知識庫文章 329204](http://go.microsoft.com/fwlink/?linkid=117786)  
  
 [設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
