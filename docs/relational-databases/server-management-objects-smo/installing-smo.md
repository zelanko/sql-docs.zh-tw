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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d6b0608265b44e7ccebd95491554739524bac390
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85894413"
---
# <a name="installing-smo"></a>安裝 SMO

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw.md)]

此頁面提供有關如何安裝 SMO 以供應用程式使用的資訊，以及使用 SMO 的系統需求。

## <a name="smo-nuget-package"></a>SMO NuGet 套件

從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017 SMO 開始，會以[SqlManagementObjects](https://www.nuget.org/packages/Microsoft.SqlServer.SqlManagementObjects) NuGet 套件的形式散發，讓使用者能夠使用 SMO 開發應用程式。

這是 SharedManagementObjects.msi 的取代，先前已發行為每個 SQL Server 版本的 SQL Feature Pack 的一部分。 使用 SMO 的應用程式應該更新為使用 NuGet 套件，而且會負責確保二進位檔會隨著開發的應用程式一起安裝。

>>[!Important]
>>如 [檔案[和版本號碼](files-and-version-numbers.md)] 頁面上所述，您不應該將 SMO 元件安裝到 GAC 中。 這麼做可能會造成其他應用程式的問題，也就是使用這些版本的 SMO （例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio）。

## <a name="installing-the-package"></a>安裝套件

如需安裝和使用 NuGet 套件的指示和範例，請參閱[NuGet 快速入門-使用套件](https://docs.microsoft.com/nuget/quickstart/use-a-package)。 
  
## <a name="system-requirements"></a>系統需求
  
 SMO 需要 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.0 或 .Net Core 2.0 才能執行，因此使用它的任何應用程式都必須確定用戶端電腦已安裝該版本或更高版本。 使用 NetFx SMO 程式庫安裝的某些原生二進位檔也需要安裝 VC 2013 執行時間;該執行時間不會包含在封裝中。 您可以從下載適用于您的目標架構的可轉散發套件https://www.microsoft.com/download/details.aspx?id=40784
  
