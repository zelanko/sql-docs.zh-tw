---
title: SQL Server 屬性 (FILESTREAM 頁面) | Microsoft Docs
description: 熟悉 SQL Server 中的 FILESTREAM 設定。 了解如何開啟 FILESTREAM，並查看如何設定遠端用戶端存取和其他屬性。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.filestream.f1
helpviewer_keywords:
- FILESTREAM [SQL Server], properties page
ms.assetid: 8a8d38d3-e97a-4b09-a40b-659b2e3a5c47
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 81edbd9bfc913f9d339625a993f866d44e1a313b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730929"
---
# <a name="server-properties---filestream-page"></a>伺服器屬性 - FILESTREAM 頁面
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  您可以使用這個頁面，針對這個 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝啟用 FILESTREAM。  
  
## <a name="ui-element-list"></a>UI 元素清單  
 **對 Transact-SQL 存取啟用 FILESTREAM**  
 選取此選項即可針對 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存取啟用 FILESTREAM。 您必須先核取這個控制項，然後才能使用其他控制選項。  
  
 **對檔案 I/O 資料流存取啟用 FILESTREAM**  
 選取此選項即可針對 Win32 資料流存取啟用 FILESTREAM。  
  
 **Windows 共用名稱**  
 使用這個控制項即可輸入即將儲存 FILESTREAM 資料之 Windows 共用的名稱。  
  
 **允許遠端用戶端具有 FILESTREAM 資料的資料流存取權**  
 選取這個控制項即可允許遠端用戶端在此伺服器上存取這項 FILESTREAM 資料。  
  
## <a name="see-also"></a>另請參閱  
 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
