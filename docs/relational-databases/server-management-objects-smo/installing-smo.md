---
title: 安裝 SMO |Microsoft 文件
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.prod_service: database-engine
ms.component: smo
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- installing SMO
- SMO [SQL Server], installing
- SQL Server Management Objects, installing
ms.assetid: 140e9971-4940-4866-89b9-5cec938e2a16
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 125712a02b362a49902c9f1e2422414f059864ef
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
#<a name="installing-smo"></a>安裝 SMO

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

此頁面提供有關如何使用安裝 SMO 應用程式和使用 SMO 的系統需求的資訊。

## <a name="smo-nuget-package"></a>SMO NuGet 封裝

開頭為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2017 SMO 散發為[Microsoft.SqlServer.SqlManagementObjects](https://www.nuget.org/packages/Microsoft.SqlServer.SqlManagementObjects) NuGet 封裝，以允許使用者使用 SMO 開發應用程式。

這是取代 SharedManagementObjects.msi，先前發行為每個版本的 SQL Server SQL Feature Pack 的一部分。 使用 SMO 應用程式應該改為使用 NuGet 套件更新，且將負責確保二進位檔案安裝與正在開發的應用程式。

>>[!Important]
>>如所述上[檔案和版本號碼](files-and-version-numbers.md) 頁面上，您不應該安裝 SMO 組件至 GAC。 如此一來可能會造成問題與其他也使用這些版本的 SMO 應用程式 (例如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Management Studio)。

##<a name="installing-the-package"></a>安裝封裝

請參閱[NuGet 快速入門-使用封裝](https://docs.microsoft.com/en-us/nuget/quickstart/use-a-package)指示和範例的安裝和使用 NuGet 封裝。 
  
## <a name="system-requirements"></a>系統需求
  
 SMO 需要[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]4.0，才能執行，因此使用它的任何應用程式必須確保用戶端電腦具有該版本或更新版本。
  
