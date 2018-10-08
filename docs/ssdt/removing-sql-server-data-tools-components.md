---
title: 移除 SQL Server Data Tools 元件 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: f8ddb919-661f-4868-8c71-87c96f1f4487
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b114b99b816e10bc004cea8d60c56d296053c7c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685466"
---
# <a name="removing-sql-server-data-tools-components"></a>移除 SQL Server Data Tools 元件
解除安裝 SSDT 或 Visual Studio 時，有些 SQL Server Data Tools (SSDT) 元件未移除。  
  
下面列出解除安裝 SSDT 或 Visual Studio 時不會從電腦中移除的 Windows Installer 套件 (.msi)。 移除這些元件會使其他 Visual Studio 版本處於不受支援的狀態。 如果您選擇移除這些元件，請使用 Windows 的 [新增或移除程式]：  
  
-   MicrosoftSQL Server Data Tools (SSDT.msi)  
  
-   MicrosoftSQL Server Data Tools Build Utilities (SSDTBuildUtilities.msi)  
  
-   SSDT 的必要條件 (SSDTDBSvcExternals.msi)  
  
下面列出其他產品可能使用且解除安裝 SSDT 後仍會保留在電腦上的共用元件。  
  
-   SQL Server 資料層應用程式架構 (DACFramework.msi)  
  
-   SQL Server 管理物件 (SharedManagementObjects.msi)  
  
-   SQL ServerTransact\-SQL 語言服務 (TSqlLanguageService.msi)  
  
-   MicrosoftSQL Server System CLR Types for SQL Server (SQLSysClrTypes.msi)  
  
-   SQL ServerTransact\-SQL ScriptDom (SQLDom.msi)  
  
-   SQL ServerTransact\-SQL Compiler Service (SQLLs.msi)  
  
