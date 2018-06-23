---
title: Syslockinfo 與 sp_lock 中之行為變更 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- syslockinfo
- sp_lock
ms.assetid: b9892ae3-ac15-48be-8b52-78dbed6467ed
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 982f31bbffb32726089fa331d105bfc262fc16a5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032207"
---
# <a name="changes-to-behavior-in-syslockinfo-and-splock"></a>syslockinfo 與 sp_lock 中之行為的變更
  **syslockinfo**和**sp_lock**可能會傳回非預期的值。 它們也可能會傳回其他資料列，而先前的版本**syslockinfo**和**sp_lock**傳回每個鎖定資源的兩個資料列的最大值。  
  
 從存取資訊**syslockinfo**或執行**sp_lock**需要在伺服器上的 VIEW SERVER STATE 權限。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 在[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]、 **syslockinfo**和**rsc_objid**中的資料行**syslockinfo**和**objid**和**indid**中的資料行**sp_lock**一致的方式傳回物件識別碼和索引識別碼。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，可能會傳回 0 值。  
  
 在[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]， **syslockinfo**和**sp_lock**最多兩個資料列的任何給定的鎖定資源傳回單一交易中。 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，啟用鎖定分割區時，可能會為單一交易底下執行的相同資源傳回多個資料列。 那里可能是 N + 1 個資料列到傳回，其中 N 是 Cpu 數目。 另外，現在還可以為相同資源顯示 GRANTED 和 WAITING 要求，而這在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中是不可行的。  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
