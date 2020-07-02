---
title: 定序和 CLR 整合資料類型 |Microsoft Docs
description: 在 SQL Server CLR 整合中，.NET Framework 字串 Api 會使用目前線程的 CultureInfo CompareInfo 屬性來執行字串比較。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- data types [CLR integration]
- parameter collation [CLR integration]
- collations [CLR integration]
ms.assetid: 6ebaed8e-2e2b-4f6d-bf4b-bc25452de441
author: rothja
ms.author: jroth
ms.openlocfilehash: e5333da328c36ed184b3e8acbbbd8671bc0b4971
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765342"
---
# <a name="collation-and-clr-integration-data-types"></a>定序和 CLR 整合資料類型
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  在中 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ， **CompareInfo**物件會處理定序。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]字串應用程式開發介面（api）會使用與目前線程的**CultureInfo**物件相關聯的**CompareInfo**屬性來執行字串比較。 **CultureInfo**物件的預設設定是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 以執行之電腦的 Windows 地區設定為基礎 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果未指定明確的**CultureInfo** ，這會決定預設的比較語義，以進行**system.string**值的比較。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不會將**CompareInfo**屬性明確地變更為資料庫或伺服器定序。 如有需要，使用者必須在其常式中設定適當的**CompareInfo**屬性。  
  
## <a name="parameter-collation"></a>參數定序  
 當您建立 common language runtime （CLR）常式，而且系結至常式的 CLR 方法的參數屬於**SQLString**類型時，會 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用包含呼叫常式之資料庫的預設定序來建立參數的實例。 如果參數不是**SqlType** （例如， **String**而非**SQLString**），則資料庫中的定序資訊不會與參數建立關聯。  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 的 SQL Server 資料類型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
