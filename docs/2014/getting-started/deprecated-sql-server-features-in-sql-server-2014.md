---
title: SQL Server 功能，SQL Server 2014 中的已被取代 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: fdc0c778-cc8d-42ab-8833-4deb4329f37a
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d28d829280e205028a99afd9fec2e019bf567ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089483"
---
# <a name="deprecated-sql-server-features-in-sql-server-2014"></a>SQL Server 2014 中已被取代的 SQL Server 功能
  此主題描述 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中仍然可用之已被取代的功能。 這些功能將在未來的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本中移除。 已被取代的功能不應在新應用程式中使用。  
  
## <a name="features-not-supported-in-the-next-version-of-includessnoversionincludesssnoversion-mdmd"></a>下一版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不支援的功能  
 下一版的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 將不再支援以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]功能。 請勿在新的開發工作中使用這些功能，並且儘速修改使用這些功能的應用程式。 「功能名稱」欄會出現在追蹤事件中當做 ObjectName，並在效能計數器和 sys.dm_os_performance_counters 中當做 instance_name。 「功能識別碼」會出現在追蹤事件中當做 ObjectId。  
  
|Category|已被取代的功能|取代|功能名稱|功能識別碼|  
|--------------|------------------------|-----------------|------------------|----------------|  
|資料可程式性|[sys.soap_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-soap-endpoints-transact-sql)|Windows Communications Foundation (WCF) 或 ASP.NET|原生 XML Web Service|22|  
|資料可程式性|[sys.endpoint_webmethods &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-catalog-views/sys-endpoint-webmethods-transact-sql)|Windows Communications Foundation (WCF) 或 ASP.NET|原生 XML Web Service|23|  
  
### <a name="slipstream-functionality"></a>匯集功能  
 產品更新功能取代了之前 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] PCU1 中可用的匯集功能。 因此的命令列參數 /*PCUSource*和 /*CUSource*，匯集功能應該不會再使用相關聯。 這些參數仍可繼續運作，但 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安裝程式的未來版本可能會移除這些參數。 /*UpdateSource*參數，結合了 「 匯集參數功能 /*PCUSource*和 /*CUSource*。  
  
 如需有關中可用的匯集功能[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]PCU1 中，請參閱 <<c2> [ 匯集 SQL Server 更新](https://go.microsoft.com/fwlink/?LinkId=219945)(https://go.microsoft.com/fwlink/?LinkId=219945) 。  
  
## <a name="see-also"></a>另請參閱  
 [回溯相容性](../../2014/getting-started/backward-compatibility.md)  
  
  
