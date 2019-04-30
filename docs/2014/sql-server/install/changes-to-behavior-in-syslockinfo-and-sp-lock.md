---
title: Syslockinfo 與 sp_lock 中之行為變更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- syslockinfo
- sp_lock
ms.assetid: b9892ae3-ac15-48be-8b52-78dbed6467ed
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4e2fa557efb6f09eae78180390c733f35bdc4a17
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63215000"
---
# <a name="changes-to-behavior-in-syslockinfo-and-splock"></a>syslockinfo 與 sp_lock 中之行為的變更
  **syslockinfo**並**sp_lock**可能會傳回非預期的值。 它們可能也會傳回額外的資料列，而先前的版本**syslockinfo**並**sp_lock**傳回每個鎖定資源的兩個資料列的最大值。  
  
 若要從存取資訊**syslockinfo**或執行**sp_lock**需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 中[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]，則**syslockinfo**並**rsc_objid**中的資料行**syslockinfo**而**objid**和**indid**中的資料行**sp_lock**一致的方式傳回的物件識別碼和索引識別碼。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，可能會傳回 0 值。  
  
 在  [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]， **syslockinfo**並**sp_lock**針對任何指定的鎖定資源的兩個資料列最多傳回單一交易中。 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，啟用鎖定分割區時，可能會為單一交易底下執行的相同資源傳回多個資料列。 那里可能是 N + 1 個資料列到傳回，其中 N 是 Cpu 數目。 另外，現在還可以為相同資源顯示 GRANTED 和 WAITING 要求，而這在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中是不可行的。  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
