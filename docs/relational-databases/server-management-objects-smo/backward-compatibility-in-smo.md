---
title: SMO 中的回溯相容性 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 2f986436-aaf2-4eaf-9809-df849d97d4fb
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 72147bbb3349839a8dd20ff7153b456f43a0c908
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86006437"
---
# <a name="backward-compatibility-in-smo"></a>SMO 中的回溯相容性
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

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
  
 如果您的程式碼使用 Urn 功能，例如**GetSqlSmoObject （Urn）**，您必須連結到 Microsoft. SqlServer。  
  
 如果您的程式碼直接使用了傳送物件，則必須連結到 Microsoft.SqlServer.Management.SmoExtended 命名空間。  
  
 當您在移轉程式碼時，可能需要修改程式碼。 這是因為有多個 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 功能都已被 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的功能取代了。 如需已被取代之功能的詳細資訊，請參閱《線上叢書》中[SQL Server 2016 的已淘汰資料庫引擎功能](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md) [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 。  
  
  
