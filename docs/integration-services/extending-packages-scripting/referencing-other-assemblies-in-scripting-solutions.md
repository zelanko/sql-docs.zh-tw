---
title: "參考其他組件中指令碼解決方案 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
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
caps.latest.revision: 68
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3deb13c7e3aeb2e974ac6e6582555a617346a298
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="referencing-other-assemblies-in-scripting-solutions"></a>參考指令碼解決方案中的其他組件
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]類別庫提供一組強大的工具與指令碼開發人員實作自訂功能[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]封裝。 指令碼工作和指令碼元件也可以使用自訂 Managed 組件。  
  
> [!NOTE]  
>  若要啟用您的封裝，以使用這些物件和方法，從 Web 服務，請使用**加入 Web 參考**中可用的命令[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA)。 在舊版的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中，您必須產生 Proxy 類別以使用 Web 服務。  
  
## <a name="using-a-managed-assembly"></a>使用 Managed 組件  
 如[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]尋找 managed 組件在設計階段，您必須執行下列步驟：  
  
1.  在電腦上的任何資料夾中儲存 Managed 組件。  
  
    > [!NOTE]  
    >  在舊版的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中，您只能加入儲存在 %windir%\Microsoft.NET\Framework\vx.x.xxxxx 資料夾或是 %ProgramFiles%\Microsoft SQL Server\100\SDK\Assemblies 資料夾中的 Managed 組件參考。  
  
2.  加入 Managed 組件的參考。  
  
     若要加入的參考，在 VSTA 中，在**加入參考**對話方塊**瀏覽**索引標籤上，找出並新增的 managed 組件。  
  
 若要 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 在執行階段尋找 Managed 組件，您必須執行下列步驟：  
  
1.  使用強式名稱簽署 Managed 組件。  
  
2.  在執行封裝的電腦上之全域組件快取中安裝組件。  
  
     如需詳細資訊，請參閱[Building，Deploying，and Debugging Custom Objects](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)。  
  
## <a name="using-the-microsoft-net-framework-class-library"></a>使用 Microsoft .NET Framework 類別庫  
 指令碼工作與指令碼元件可以利用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 類別庫公開的所有其他物件與功能。 例如，透過使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]，可以擷取您的環境相關資訊，並與執行封裝的電腦互動。  
  
 這個清單說明幾個較常使用的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 類別：  
  
-   **System.Data**包含 ADO.NET 架構。  
  
-   **System.IO**提供檔案系統和資料流的介面。  
  
-   **System.Windows.Forms**提供表單建立。  
  
-   **System.Text.RegularExpressions**提供類別來使用規則運算式。  
  
-   **System.Environment**傳回本機電腦、 目前的使用者和電腦和使用者設定的相關資訊。  
  
-   **System.Net**提供網路通訊。  
  
-   **System.DirectoryServices** ： 公開 Active Directory。  
  
-   **System.Drawing**提供大量的影像操作程式庫。  
  
-   **System.Threading**可讓多執行緒的程式設計。  
  
 如需有關 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 的相細資訊，請參閱 MSDN Library。  
  
## <a name="see-also"></a>另請參閱  
 [使用指令碼擴充封裝](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
  
  
