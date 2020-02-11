---
title: Syslockinfo 和 sp_lock 中行為的變更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- syslockinfo
- sp_lock
ms.assetid: b9892ae3-ac15-48be-8b52-78dbed6467ed
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e8c6534449ffc4e89efcd49c943726bf6ecd9f26
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66096650"
---
# <a name="changes-to-behavior-in-syslockinfo-and-sp_lock"></a>syslockinfo 與 sp_lock 中之行為的變更
  **syslockinfo**和**sp_lock**可能會傳回非預期的值。 它們也可能會傳回額外的資料列，而舊版的**syslockinfo**和**sp_lock**則會針對每個鎖定資源傳回最多兩個數據列。  
  
 若要從**syslockinfo**或執行**sp_lock**存取訊號，需要伺服器的 VIEW SERVER STATE 許可權。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 在[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]中， **syslockinfo**中的**rsc_objid**和**rsc_indid**資料行以及**sp_lock**中的**objid**和**indid**資料行一致地傳回物件識別碼和索引識別碼。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，可能會傳回 0 值。  
  
 在[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]中， **syslockinfo**和**sp_lock**會針對單一交易中的任何指定鎖定資源，傳回最多兩個數據列。 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，啟用鎖定分割區時，可能會為單一交易底下執行的相同資源傳回多個資料列。 最多可能會傳回 N + 1 個數據列，其中 N 是 Cpu 的數目。 另外，現在還可以為相同資源顯示 GRANTED 和 WAITING 要求，而這在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中是不可行的。  
  
## <a name="permissions"></a>權限  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
