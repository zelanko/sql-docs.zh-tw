---
title: 安裝 SMO |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- installing SMO
- SMO [SQL Server], installing
- SQL Server Management Objects, installing
ms.assetid: 140e9971-4940-4866-89b9-5cec938e2a16
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 15f862ceff618fb3c0f20d6e2bdf8d9d5b276801
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47806836"
---
#<a name="installing-smo"></a>安裝 SMO

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

此頁面提供有關如何安裝使用 SMO 應用程式和使用 SMO 的系統需求的資訊。

## <a name="smo-nuget-package"></a>SMO NuGet 套件

開頭[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]形式散發 2017 SMO [Microsoft.SqlServer.SqlManagementObjects](https://www.nuget.org/packages/Microsoft.SqlServer.SqlManagementObjects) NuGet 套件，可讓使用者使用 SMO 開發應用程式。

這是取代 SharedManagementObjects.msi，先前發行為每個版本的 SQL Server SQL Feature Pack 的一部分。 使用 SMO 應用程式應該要改為使用 NuGet 套件更新，而且會負責確保二進位碼檔案會隨正在開發的應用程式。

>>[!Important]
>>上所述[檔案和版本號碼](files-and-version-numbers.md) 頁面上，您不應該安裝 SMO 組件到 GAC。 如此一來可能會造成問題與其他應用程式也使用 SMO 的這些版本 (例如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Management Studio)。

##<a name="installing-the-package"></a>安裝套件

請參閱[NuGet 快速入門-使用套件](https://docs.microsoft.com/nuget/quickstart/use-a-package)指示和範例的安裝與使用 NuGet 套件。 
  
## <a name="system-requirements"></a>系統需求
  
 SMO 需要[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]4.0，才能執行，所以使用它的任何應用程式必須確定用戶端電腦有該版本或更新版本。
  
