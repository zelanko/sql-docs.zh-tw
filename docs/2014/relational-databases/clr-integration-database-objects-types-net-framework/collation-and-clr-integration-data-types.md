---
title: 定序和 CLR 整合資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data types [CLR integration]
- parameter collation [CLR integration]
- collations [CLR integration]
ms.assetid: 6ebaed8e-2e2b-4f6d-bf4b-bc25452de441
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 56206f6273b413a66a72b2a2c72ed3593b2f9a66
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37354680"
---
# <a name="collation-and-clr-integration-data-types"></a>定序和 CLR 整合資料類型
  在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中，`CompareInfo` 物件會處理定序。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 字串應用程式開發介面 (API) 會使用與目前執行緒之 `CompareInfo` 物件相關聯的 `CultureInfo` 屬性來執行字串比較。 預設值`CultureInfo`物件根據[!INCLUDE[msCoName](../../includes/msconame-md.md)]的電腦上的 Windows 地區設定[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在執行。 如果沒有指定任何明確的 `CultureInfo`，這會決定預設的比較語意來比較 `System.String` 值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會將 `CompareInfo` 屬性明確地變更為資料庫或伺服器定序。 如有需要，使用者必須在其常式中設定適當的 `CompareInfo` 屬性。  
  
## <a name="parameter-collation"></a>參數定序  
 當您建立 Common Language Runtime (CLR) 常式，而且繫結至常式的 CLR 方法參數類型為 `SQLString` 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用包含呼叫常式之資料庫的預設定序建立參數的執行個體。 如果參數不是 `SqlType` (例如，`String` 而非 `SQLString`)，資料庫中的定序資訊不會與參數相關聯。  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 的 SQL Server 資料類型](sql-server-data-types-in-the-net-framework.md)  
  
  
