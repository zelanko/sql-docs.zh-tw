---
title: SQL Server 2014 中已淘汰的 SQL Server 功能 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: fdc0c778-cc8d-42ab-8833-4deb4329f37a
author: rothja
ms.author: jroth
ms.openlocfilehash: 7e4d888eee5ea6048d61007728bb436dabdccb8e
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84926979"
---
# <a name="deprecated-sql-server-features-in-sql-server-2014"></a>SQL Server 2014 中已被取代的 SQL Server 功能
  此主題描述 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中仍然可用之已被取代的功能。 這些功能將在未來的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本中移除。 已被取代的功能不應在新應用程式中使用。  
  
## <a name="features-not-supported-in-the-next-version-of-ssnoversion"></a>下一版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不支援的功能  
 下一版的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 將不再支援以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]功能。 請勿在新的開發工作中使用這些功能，並且儘速修改使用這些功能的應用程式。 「功能名稱」欄會出現在追蹤事件中當做 ObjectName，並在效能計數器和 sys.dm_os_performance_counters 中當做 instance_name。 「功能識別碼」會出現在追蹤事件中當做 ObjectId。  
  
|類別|已被取代的功能|取代|功能名稱|功能識別碼|  
|--------------|------------------------|-----------------|------------------|----------------|  
|資料可程式性|[soap_endpoints &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-soap-endpoints-transact-sql)|Windows Communications Foundation (WCF) 或 ASP.NET|原生 XML Web Service|22|  
|資料可程式性|[endpoint_webmethods &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-endpoint-webmethods-transact-sql)|Windows Communications Foundation (WCF) 或 ASP.NET|原生 XML Web Service|23|  
  
### <a name="slipstream-functionality"></a>匯集功能  
 [產品更新功能](/previous-versions/sql/sql-server-2012/hh231670(v=sql.110)?redirectedfrom=MSDN)已在 SQL Server 2012 中引進，做為 PCU1 中所提供彙集功能的延伸模組 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 。 在 SQL Server 2014 中，產品更新功能是用於彙集 SQL Server 的建議方法。 因此，不應再使用與原始彙集功能相關聯的命令列參數、/*PCUSource*和/*CUSource*。 這些參數將會繼續作用，但在未來的安裝程式版本中可能會移除 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 建議使用的參數是/*UpdateSource* ，其結合了原始彙集參數、/*PCUSource*和/*CUSource*的功能。  
  
 如需 PCU1 中可用彙集功能的詳細資訊 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] ，請參閱彙集[SQL Server 更新](https://go.microsoft.com/fwlink/?LinkId=219945)（ https://go.microsoft.com/fwlink/?LinkId=219945) 。  
 如需如何使用/*UpdateSource*來彙集 SQL Server 組建的詳細資訊，請參閱下列各項：
 
 - [如何使用更新的安裝程式套件修補 SQL Server 2012 安裝程式（使用 UpdateSource 取得智慧型設定）](https://blogs.msdn.microsoft.com/jason_howell/2012/08/28/how-to-patch-sql-server-2012-setup-with-an-updated-setup-package-using-updatesource-to-get-a-smart-setup/)
 
 - [SQL Server 2012 安裝程式變得更聰明 .。。](https://techcommunity.microsoft.com/t5/SQL-Server-Support/SQL-Server-2012-Setup-just-got-smarter-8230/ba-p/317440)
 
## <a name="see-also"></a>另請參閱  
 [回溯相容性](../../2014/getting-started/backward-compatibility.md)  
  
  
