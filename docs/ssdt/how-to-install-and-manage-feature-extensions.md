---
title: 如何：安裝和管理擴充功能 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 04/26/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9cdc8cd5-c36f-4bee-a191-87ed457803e7
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b3d6d4c85a287dc000d761df1eafeb49e4261336
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093862"
---
# <a name="how-to-install-and-manage-feature-extensions"></a>如何：安裝和管理擴充功能
您可以新增規則，以分析資料庫程式碼、資料庫單元測試的條件，以及建置/部署參與者，來增加 Visual Studio 版本 (包括 SQL Server Data Tools) 提供的功能。 不過，無論您已建立擴充功能或已安裝其他人建立的擴充功能，都必須先安裝擴充功能，才能使用它。  
  
安裝擴充功能的位置視擴充功能類型，以及您打算從哪裡使用它而定。 在最新版的 Visual Studio 中，部分元件的安裝位置已從 SQL Server 安裝目錄移至 Visual Studio 目錄內。 此設定可讓不同版本的軟體更容易並列執行，但其表示，如果您想要在不同版本的 SQL Server Data Tools 中，以及從命令列中使用擴充功能，則可能需要在多個位置中安裝它。  
  
### <a name="installing-extensions-for-use-inside-visual-studio"></a>安裝要在 Visual Studio 內使用的擴充功能  
  
|擴充功能類型|安裝位置|  
|------------------|--------------------|  
|SQL Server 單元測試的自訂測試條件|<Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\TestConditions|  
|建置參與者<br /><br />部署參與者<br /><br />靜態程式碼分析規則|<Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\DAC\120\Extensions|  
  
<Visual Studio Install Dir> 將視您使用的 Visual Studio 版本和所選擇安裝的位置而有所不同。 針對 Visual Studio 2012，通常是 C:\Program Files (x86)\\MicrosoftVisual Studio 11.0。 針對 Visual Studio 2013， 通常是 C:\Program Files (x86)\\MicrosoftVisual Studio 12.0。  
  
擴充功能可以當做我們的命令列服務的一部分執行：  
  
|擴充功能類型|命令列服務|安裝資料夾|  
|------------------|------------------------|------------------|  
|SQL Server 單元測試的自訂測試條件|MSBuild / MSTest 可以用來從 Visual Studio 2013 開發人員命令提示字元和類似命令列工具執行單元測試。|與在 Visual Studio 內執行時相同。|  
|建置參與者<br /><br />部署參與者|[SqlPackage.exe](../tools/sqlpackage.md)，或在建置資料庫專案時使用 MSBuild 部署或發行目標。|MSBuild：與在 Visual Studio 內執行時相同。<br /><br />[SqlPackage.exe](../tools/sqlpackage.md)：如果位於 Visual Studio 目錄中，則與先前相同。<br /><br />如果 SqlPackage.exe 和其他 DacFx DLL 位於該目錄外，則擴充功能應該放置在相同目錄，或放置在 C:\Program Files (x86)\\MicrosoftSQL Server\120\DAC\bin\Extensions 中。|  
|靜態程式碼分析規則|MSBuild 可以用來建置專案，並執行靜態程式碼分析。<br /><br />此外，您也可以從自己的應用程式使用 CodeAnalysisService API 來執行程式碼分析。 在此情況下，擴充功能查閱規則的運作方式與使用 SqlPackage.exe 的方式相同。|對建置參與者和部署參與者皆相同|  
  
> [!NOTE]  
> 您必須對電腦具有系統管理員權限，才能存取 Program Files 資料夾下的任一安裝目錄。 如果沒有適當的權限，請連絡網路管理員。  
  
**安全性考量**  
  
安裝不是您建立的擴充功能之前，必須了解下列風險：  
  
-   擴充功能的安裝程式可能是惡意程式，會根據您的安裝權限存取受保護的資源。  
  
-   擴充功能本身可能是惡意的，如果使用擴充功能的使用者有足夠的權限，它就會取得受保護資源的控制權。  
  
為了降低您的風險，只在擴充功能來自已知來源時，才予以安裝。 如果您從未受信任的來源取得擴充功能，應該檢查該擴充功能的原始程式碼及其安裝程式 (如果有)，然後進行安裝並使用該擴充功能。  
  
## <a name="to-install-a-custom-feature-extension"></a>安裝自訂擴充功能  
將已簽署的組件 (.dll) 複製至正確的安裝資料夾。 關閉並重新開啟 Visual Studio。 現在應該可以使用擴充功能。  
  
## <a name="see-also"></a>另請參閱  
[擴充資料庫功能](../ssdt/extending-the-database-features.md)  
  
