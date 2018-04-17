---
title: 定序和 CLR 整合資料類型 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
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
ms.workload: Inactive
ms.openlocfilehash: 617c8dea3844f1b2ae980775949d4d1c793b4f1a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="collation-and-clr-integration-data-types"></a>定序和 CLR 整合資料類型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]、 **compareinfo 一起**物件會處理定序。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]字串應用程式開發介面 (Api) 使用**compareinfo 一起**屬性相關聯**CultureInfo**目前的執行緒來執行字串比較的物件。 預設值為**CultureInfo**物件根據[!INCLUDE[msCoName](../../includes/msconame-md.md)]所在之電腦的 Windows 地區設定[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在執行。 這會決定預設的比較語意，如果任何明確**CultureInfo** ，為指定的比較**System.String**值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 明確地變更**compareinfo 一起**為資料庫或伺服器定序屬性。 必要時，使用者必須將適當**compareinfo 一起**在其常式中的屬性。  
  
## <a name="parameter-collation"></a>參數定序  
 當您建立 common language runtime (CLR) 常式，並 CLR 方法的參數繫結至常式具型別的**SQLString**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立參數的執行個體之資料庫的預設定序包含呼叫常式。 如果參數不是**SqlType** (例如，**字串**而**SQLString**)，從資料庫的定序資訊不是與參數相關聯。  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 中的 SQL Server 資料類型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
