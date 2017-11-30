---
title: "SQL Server 2016 中的 SQL Server Reporting Services 重大變更 | Microsoft Docs"
ms.date: 07/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Me.Value references
- Reporting Services, backward compatibility
- breaking changes [Reporting Services]
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
caps.latest.revision: "121"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c82355e6ceb86d20bc17747edf637e4ddd2a440b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="breaking-changes-in-sql-server-reporting-services-in-sql-server-2016"></a>SQL Server 2016 中 SQL Server Reporting Services 的重大變更

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../includes/ssrs-previous-versions.md)]

本主題描述 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中的重大變更。 這些變更可能會中斷以舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]為根據的應用程式、指令碼或功能。 當您進行升級或是在自訂指令碼或報表內時，可能會遇到這些問題。

## <a name="security-extensions"></a>安全性延伸模組

自訂安全性延伸模組需要做一些修改，才能使用新的 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]。 安全性延伸模組必須使用 IAuthenticationExtension2 介面。

## <a name="wmi-provider"></a>WMI 提供者

[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 應用程式名稱從 "ReportManager" 變更為 "ReportServerWebApp"。

## <a name="next-steps"></a>後續的步驟

[SQL Server 2016 中的 SQL Server Reporting Services 行為變更](../reporting-services/behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)  
[Reporting Services (SSRS) 的新功能](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)   
[SQL Server 2016 中 SQL Server Reporting Services 已被取代的功能](../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)    
[SQL Server 2016 中的 SQL Server Reporting Services 已中止功能](../reporting-services/discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
