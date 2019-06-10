---
title: access check cache 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- access check cache option
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: cc290a3fbde8426c1728a03b4ec9ddeaf4d5144f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66782476"
---
# <a name="access-check-cache-server-configuration-options"></a>存取檢查快取伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  當資料庫物件是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所存取時，存取檢查會在稱為 **access check result cache**的內部結構中進行快取。 **access check cache quota** 和 **access check cache bucket count** 選項會控制用於 **access check result cache**的項目數和雜湊值區數。 在罕見的情況下，可以變更這些選項來提升效能。  
  
 預設值 0 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在管理這些選項。 Microsoft 建議只要變更 Microsoft 客戶支援服務所導向的那些選項。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
