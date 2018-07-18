---
title: SQL Server 功能，SQL Server 2014 中的已被取代 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fdc0c778-cc8d-42ab-8833-4deb4329f37a
caps.latest.revision: 20
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7d47249b2263ea3d5523458fd34770e7c009800
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37324728"
---
# <a name="deprecated-sql-server-features-in-sql-server-2014"></a>SQL Server 2014 中已被取代的 SQL Server 功能
  此主題描述 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中仍然可用之已被取代的功能。 這些功能將在未來的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本中移除。 已被取代的功能不應在新應用程式中使用。  
  
## <a name="features-not-supported-in-the-next-version-of-includessnoversionincludesssnoversion-mdmd"></a>下一版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不支援的功能  
 下一版的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 將不再支援以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]功能。 請勿在新的開發工作中使用這些功能，並且儘速修改使用這些功能的應用程式。 「功能名稱」欄會出現在追蹤事件中當做 ObjectName，並在效能計數器和 sys.dm_os_performance_counters 中當做 instance_name。 「功能識別碼」會出現在追蹤事件中當做 ObjectId。  
  
|類別目錄|已被取代的功能|取代|功能名稱|功能識別碼|  
|--------------|------------------------|-----------------|------------------|----------------|  
|資料可程式性|[sys.soap_endpoints &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-catalog-views/sys-soap-endpoints-transact-sql)|Windows Communications Foundation (WCF) 或 ASP.NET|原生 XML Web Service|22|  
|資料可程式性|[sys.endpoint_webmethods &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-catalog-views/sys-endpoint-webmethods-transact-sql)|Windows Communications Foundation (WCF) 或 ASP.NET|原生 XML Web Service|23|  
  
### <a name="slipstream-functionality"></a>匯集功能  
 產品更新功能取代了之前 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] PCU1 中可用的匯集功能。 因此的命令列參數 /*PCUSource*和 /*CUSource*，匯集功能應該不會再使用相關聯。 這些參數仍可繼續運作，但 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安裝程式的未來版本可能會移除這些參數。 /*UpdateSource*參數，結合了 「 匯集參數功能 /*PCUSource*和 /*CUSource*。  
  
 如需有關中可用的匯集功能[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]PCU1 中，請參閱 <<c2> [ 匯集 SQL Server 更新](http://go.microsoft.com/fwlink/?LinkId=219945)(http://go.microsoft.com/fwlink/?LinkId=219945)。  
  
## <a name="see-also"></a>另請參閱  
 [回溯相容性](../../2014/getting-started/backward-compatibility.md)  
  
  
