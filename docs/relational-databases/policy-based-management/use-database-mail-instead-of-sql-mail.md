---
title: 使用 Database Mail 取代 SQL Mail | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: b08df7be-d8be-4184-a661-38ec0ac85cd1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c029883591c49c1be52d23a025ff522b4095a6f5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68069147"
---
# <a name="use-database-mail-instead-of-sql-mail"></a>使用 Database Mail 而非 SQL Mail
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此規則會檢查 sys.configurations 目錄檢視，以判斷 SQL Mail XP 的整個伺服器組態選項是否設定為 ON。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的未來版本將移除 SQL Mail。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 若要傳送郵件，請使用 Database Mail。  
  
 SQL Mail 會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的同處理序執行。 如果 SQL Mail 關閉，伺服器也會關閉。 Database Mail 會在不同處理序的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 外部執行，它可以擴充，而且不需要在實際執行伺服器上安裝延伸的 MAPI 用戶端元件。  
  
## <a name="for-more-information"></a>詳細資訊  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
