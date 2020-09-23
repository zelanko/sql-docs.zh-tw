---
description: 在 SQL Server Management Studio (SSMS) 中安裝延伸模組
title: 在 SQL Server Management Studio (SSMS) 中安裝延伸模組
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
keywords:
- 擴充功能
- vsix
- 安裝延伸模組
- 安裝 VSIX
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: seo-lt-2019
ms.date: 07/29/2020
ms.openlocfilehash: bf4c9ee5287a2e0fdecf8455334561ce130499bc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492026"
---
# <a name="install-extensions-in-sql-server-management-studio-ssms"></a>在 SQL Server Management Studio (SSMS) 中安裝延伸模組

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

SQL Server Management Studio (SSMS) 延伸模組是使用 C# 透過 Visual Studio 中的「Visual Studio 延伸模組開發」工作負載建立的。 SSMS 18.x 是在 Visual Studio 2017 Shell 上建置的，須遵循該環境的限制。

透過 Visual Studio 或獨立的受控套件安裝程式來部署 VSIX，即可在 SSMS 18.x 中安裝延伸模組。  Visual Studio 部署程序如下所述。

> [!NOTE]
> 在 SSMS 18.x 下，無法透過 VSIXInstaller 安裝 SQL Server Management Studio 延伸模組。
  
## <a name="visual-studio-deployment-of-an-extension-for-ssms-18x"></a>SSMS 18.x 延伸模組的 Visual Studio 部署

延伸模組的手動安裝，可藉由將相關聯的延伸模組檔案 (VSIX) 複製到預設的 SSMS 延伸模組資料夾中來完成。  SSMS 在啟動時會自動檢查此資料夾中的延伸模組。  Visual Studio 可在專案建置階段完成 VSIX 部署。 

  
1.  找出您的 SSMS 安裝和預設的延伸模組資料夾。  使用預設 SSMS 安裝設定時，資料夾位置為 ```C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\Extensions\```。  


2. 以系統管理員身分啟動 Visual Studio。

3.  藉由在專案屬性視窗的 [VSIX] 索引標籤中核取 [將 VSIX 內容複寫至下列位置] 核取方塊，即可在建置期間由 Visual Studio 完成檔案複製程序。 在此核取方塊下方的文字方塊中，輸入前述的資料夾位置，並附加此延伸模組的資料夾。  例如：```C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\Extensions\SampleExtension```
  
![具有 3 個核取方塊和一個文字方塊的專案屬性視窗 VSIX 設定](./media/install-extensions/vsix_ssms.png)

4. 建置延伸模組專案，成功的建置會將延伸模組檔案傳輸至 SSMS 延伸模組資料夾。

5.  啟動 SSMS 並測試延伸模組的功能。
  
