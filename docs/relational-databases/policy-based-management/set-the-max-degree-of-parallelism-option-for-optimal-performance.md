---
title: 平行處理原則的最大程度和原則式管理
description: 描述如何設定原則，以驗證 SQL Server 原則式管理的平行處理原則最大程度值。
ms.custom: seo-lt-2019
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: a03a0236c177605bf5041e92ea9c19708d5bc9ae
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "75776367"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>設定平行處理原則的最大程度選項來取得最佳效能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此規則會判斷某個值的 max degree of parallelism (MAXDOP) 選項是否大於 8。 將這個選項設定為較大的值通常會造成不必要的資源耗用，而且會降低效能。  
  
## <a name="best-practice-recommendations"></a>最佳做法建議  
 平行處理原則的最大程度 (MAXDOP) 組態選項，可控制在平行計劃中執行查詢時所使用的處理器數目。 此選項可決定用於平行執行工作的查詢計劃運算子執行緒數目。 您必須根據 SQL Server 設定位置 (在對稱式多處理 (SMP) 電腦、非統一記憶體存取 (NUMA) 電腦或已啟用超執行緒的處理器上)，相應設定 [平行處理原則的最大程度] 選項。 
 
 MAXDOP 的設定建議取決於您所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。 如需特定版本的指導方針，請參閱[設定 [平行處理原則的最大程度] 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)，並設定原則以據此驗證 [平行處理原則的最大程度] 值。     
  
## <a name="for-more-information"></a>取得詳細資訊  
 [SQL Server 中平行處理原則最大程度組態選項的建議和指導方針](https://go.microsoft.com/fwlink/?linkid=117786)    
 [設定平行處理原則最大程度伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)     
  
