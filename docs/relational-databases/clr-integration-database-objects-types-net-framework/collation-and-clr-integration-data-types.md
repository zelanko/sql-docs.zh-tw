---
title: 定序和 CLR 整合資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
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
ms.openlocfilehash: 31bb87caa5d5b997c3e99478fc3308fc03d4f956
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37357700"
---
# <a name="collation-and-clr-integration-data-types"></a>定序和 CLR 整合資料類型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]，則**Compareinfo&lt**物件會處理定序。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]字串應用程式開發介面 (Api) 使用**Cultureinfo.invariantculture**相關聯的屬性**CultureInfo**目前的執行緒來執行字串比較的物件。 預設值**CultureInfo**物件依據[!INCLUDE[msCoName](../../includes/msconame-md.md)]所在之電腦的 Windows 地區設定[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在執行。 如果不明確，這會決定預設的比較語意**CultureInfo**指定，來比較**System.String**值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會明確地變更**Cultureinfo.invariantculture**為資料庫或伺服器定序的屬性。 如有需要，使用者必須設定適當**Cultureinfo.invariantculture**在其常式中的屬性。  
  
## <a name="parameter-collation"></a>參數定序  
 當您建立 common language runtime (CLR) 常式，而且 CLR 方法的參數繫結至常式具型別的**SQLString**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立參數的執行個體之資料庫的預設定序包含呼叫常式。 如果參數不是**SqlType** (例如**字串**而非**SQLString**)，從資料庫的定序資訊不是與參數相關聯。  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 的 SQL Server 資料類型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
