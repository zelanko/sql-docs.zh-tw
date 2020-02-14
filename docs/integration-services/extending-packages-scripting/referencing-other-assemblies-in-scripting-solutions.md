---
title: 參考指令碼解決方案中的其他組件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, .NET Framework
- Script task [Integration Services], adding references
- referencing custom assemblies
- SSIS Script task, VisualBasic namespace
- assemblies [Integration Services]
- VisualBasic namespace
- Script task [Integration Services], VisualBasic namespace
- Microsoft.VisualBasic namespace
- Script task [Integration Services], .NET Framework
- .NET Framework [Integration Services]
- referencing Web services
ms.assetid: 9b655bcd-19f6-43d8-9f89-1b4d299c6380
author: chugugrace
ms.author: chugu
ms.openlocfilehash: aa693a941ed5f6d56952c4e720aba7dc318600e0
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71286270"
---
# <a name="referencing-other-assemblies-in-scripting-solutions"></a>參考指令碼解決方案中的其他組件

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 類別庫提供指令碼開發人員一組強大的工具，以實作 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件中的自訂功能。 指令碼工作和指令碼元件也可以使用自訂 Managed 組件。  
  
> [!NOTE]
>  若要讓您的封裝能夠使用 Web 服務中的物件和方法，請使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 所提供的 [加入 Web 參考]  命令。 在舊版的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中，您必須產生 Proxy 類別以使用 Web 服務。  
  
## <a name="using-a-managed-assembly"></a>使用 Managed 組件  
 若要讓 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 在設計階段尋找 Managed 組件，您必須執行下列步驟：  
  
1.  在電腦上的任何資料夾中儲存 Managed 組件。  
  
    > [!NOTE]  
    >  在舊版的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中，您只能加入儲存在 %windir%\Microsoft.NET\Framework\vx.x.xxxxx 資料夾或是 %ProgramFiles%\Microsoft SQL Server\100\SDK\Assemblies 資料夾中的 Managed 組件參考。  
  
2.  加入 Managed 組件的參考。  
  
     若要加入參考，請在 VSTA 中，於 [加入參考]  對話方塊的 [瀏覽]  索引標籤上，找到並加入 Managed 組件。  
  
 若要 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 在執行階段尋找 Managed 組件，您必須執行下列步驟：  
  
1.  使用強式名稱簽署 Managed 組件。  
  
2.  在執行封裝的電腦上之全域組件快取中安裝組件。  
  
     如需詳細資訊，請參閱[建立、部署和偵錯自訂物件](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)。  
  
## <a name="using-the-microsoft-net-framework-class-library"></a>使用 Microsoft .NET Framework 類別庫  
 指令碼工作與指令碼元件可以利用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 類別庫公開的所有其他物件與功能。 例如，透過使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]，可以擷取您的環境相關資訊，並與執行封裝的電腦互動。  
  
 這個清單說明幾個較常使用的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 類別：  
  
-   **System.Data**：包含 ADO.NET 架構。  
  
-   **System.IO**：提供介面給檔案系統與資料流。  
  
-   **System.Windows.Forms**：提供表單建立。  
  
-   **System.Text.RegularExpressions**：提供可使用規則運算式的類別。  
  
-   **System.Environment**：傳回有關本機電腦、目前使用者以及電腦與使用者設定的資訊。  
  
-   **System.Net**：提供網路通訊。  
  
-   **System.DirectoryServices**： 公開 Active Directory。  
  
-   **System.Drawing**：提供大量的影像操作程式庫。  
  
-   **System.Threading**：允許多執行緒程式設計。  
  
 如需有關 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 的相細資訊，請參閱 MSDN Library。  
  
## <a name="see-also"></a>另請參閱  
 [使用指令碼擴充套件](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
  
  
