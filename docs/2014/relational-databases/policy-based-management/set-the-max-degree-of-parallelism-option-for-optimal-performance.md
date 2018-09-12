---
title: 設定平行處理原則的最大程度選項來取得最佳效能 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3f11fb308bd9543c01bc41b43aa8f10a259922e9
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43812324"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>設定平行處理原則的最大程度選項來取得最佳效能
  此規則會判斷某個值的 max degree of parallelism (MAXDOP) 選項是否大於 8。 將這個選項設定為較大的值通常會造成不必要的資源耗用，而且會降低效能。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 使用 sp_configure 將 max degree of parallelism 選項設定為 8。  
  
## <a name="for-more-information"></a>詳細資訊  
 [Microsoft 知識庫文章 329204](http://go.microsoft.com/fwlink/?linkid=117786)  
  
 [設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
