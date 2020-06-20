---
title: SMO 中的回溯相容性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 2f986436-aaf2-4eaf-9809-df849d97d4fb
author: stevestein
ms.author: sstein
ms.openlocfilehash: fe4a3e1c9a49737f06425c6e8bd651e5e973e77b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055297"
---
# <a name="backward-compatibility-in-smo"></a>SMO 中的回溯相容性
  以舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 撰寫的 SMO 應用程式可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的 SMO 重新編譯。  
  
## <a name="migrating-smo-applications"></a>移轉 SMO 應用程式  
 您必須移除舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之 SMO dll 的參考，並納入 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 所提供之新 SMO dll 的參考。  
  
 下列是您應該要參考的基本項目：  
  
-   Microsoft.SqlServer.ConnectionInfo  
  
-   Microsoft.SqlServer.Smo  
  
-   Microsoft.SqlServer.Management.Sdk.Sfc  
  
 對於連接類別、SMO 公用程式類別和基礎類別而言，這些檔案是必須的。  
  
> [!NOTE]  
>  由於 SmoEnum.dll 已經移除，因此所有指向它的參考也必須從 SMO [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 專案中移除。  
  
 命名空間也已變更，因此您可以使用下列的命名空間：  
  
##### <a name="for-visual-c"></a>For Visual C#  
  
```  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Common;  
```  
  
##### <a name="for-visual-basic"></a>For Visual Basic  
  
```  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Common  
```  
  
 如果您的程式碼使用了 Urn 功能，例如 `Server.GetSqlSmoObject(Urn)`，則必須連結到 Microsoft.SqlServer.Management.Sdk.Sfc 命名空間。  
  
 如果您的程式碼直接使用了傳送物件，則必須連結到 Microsoft.SqlServer.Management.SmoExtended 命名空間。  
  
 當您在移轉程式碼時，可能需要修改程式碼。 這是因為有多個 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 功能都已被 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的功能取代了。 如需已被取代之功能的詳細資訊，請參閱《線上叢書》中[SQL Server 2014 的已淘汰資料庫引擎功能](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md) [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 。  
  
  
