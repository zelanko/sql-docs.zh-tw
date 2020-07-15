---
title: 將 PAGE_VERIFY 資料庫選項設定為 CHECKSUM | Microsoft 文件
description: 檢查 PAGE_VERIFY 選項是否為 CHECKSUM，此選項會控制 SQL Server 資料庫引擎是否會計算總和檢查碼來協助提供資料檔案完整性。
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 686b9a4a-ea61-4263-9ab8-f444a3077679
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 5f296dc9aedf96c3258dc256d9bc8fc8fdf05f12
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774176"
---
# <a name="set-the-page_verify-database-option-to-checksum"></a>將 PAGE_VERIFY 資料庫選項設定為 CHECKSUM
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  這個規則會檢查 PAGE_VERIFY 資料庫選項是否設定為 CHECKSUM。 當針對 PAGE_VERIFY 資料庫選項啟用 CHECKSUM 時， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會針對整頁的內容計算總和檢查碼，並在將頁面寫入磁碟時，於頁首中儲存值。 從磁碟讀取頁面時，會重新計算總和檢查碼，並與頁首所儲存的總和檢查碼值作比較。 如此有助於提供高層級的資料檔完整性。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 將 PAGE_VERIFY 資料庫選項設定為 CHECKSUM。  
  
## <a name="for-more-information"></a>詳細資訊  
 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
