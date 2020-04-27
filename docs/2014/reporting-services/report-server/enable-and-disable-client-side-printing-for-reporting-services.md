---
title: 啟用和停用 Reporting Services 的用戶端列印功能 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 0e709c96-7517-4547-8ef6-5632f8118524
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ea5016aa51a25bd296d2e77516b30b84a7a28cec
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66103924"
---
# <a name="enable-and-disable-client-side-printing-for-reporting-services"></a>啟用和停用 Reporting Services 的用戶端列印功能
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX 控制項（ **RSClientPrint**）會針對瀏覽器中所查看的報表，提供用戶端列印功能。 此控制項會顯示自訂列印對話方塊，其中支援與其他列印對話方塊一樣的一般功能。 這些功能包括預覽列印、可指定要列印的特定頁面及範圍、頁面邊界和列印方向。 雖然依預設會啟用用戶端列印，但如果您不想提供此功能，也可以停用它。  
  
> [!NOTE]  
>  下載 ActiveX 控制項需要具有管理員權限。  
  
## <a name="downloading-the-activex-control"></a>下載 ActiveX 控制項  
 每一個想要使用列印功能的使用者，都必須下載並安裝提供用戶端列印功能的 ActiveX 控制項。 使用者第一次按一下 [報表] 工具列上的 [**印表機**] 圖示時，會將 Microsoft ActiveX 控制項下載至電腦。 下載控制項之後，每當使用者按一下**印表機**圖示時，就會顯示 [**列印**] 對話方塊。  
  
 視瀏覽器設定而定，也許會提示使用者安裝此控制項、防止安裝此控制項，或在背景中無障礙地安裝此控制項。  
  
 對於[!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer，影響 activex 控制項下載和安裝的設定是透過 Web 內容區域之 [**安全性設定**] 頁面中的 [ **ActiveX 控制項與外掛程式]** 節點來指定。 下列設定將根據網際網路區域安全性喜好設定，決定使用者是否可以下載及執行列印控制項：  
  
-   下載簽署的 ActiveX 控制項。  
  
-   為標示為安全可供撰寫指令碼的 ActiveX 控制項撰寫指令碼。  
  
-   執行 ActiveX 控制項和外掛程式。  
  
 想要使用**RSClientPrint**執行用戶端列印的使用者必須啟用下列功能：  
  
-   **下載已簽署的 activex 控制項**，並**編寫標示為安全的 activex 控制項腳本**，以供安裝之用。  
  
-   **執行 ActiveX 控制項和外掛程式**進行進行中的列印工作。  
  
 **RSClientPrint** ActiveX 控制項已簽署，這表示它包含來自[!INCLUDE[msCoName](../../includes/msconame-md.md)]的有效數位憑證。  
  
## <a name="enabling-and-disabling-client-side-printing"></a>啟用及停用用戶端列印  
 報表伺服器管理員可以選擇停用列印功能，方法是將報表伺服器系統屬性**EnableClientPrinting**設定為`false`。 這樣會停用由該伺服器管理的所有報表的用戶端列印功能。 根據預設， **EnableClientPrinting**會設定為`true`。 您可以採用下列方式來停用用戶端列印：  
  
-   針對 **原生模式報表伺服器**：  
  
    1.  使用系統管理權限來啟動 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 。  
  
    2.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，連接到報表伺服器執行個體。  
  
    3.  以滑鼠右鍵按一下報表伺服器節點，然後按一下 [屬性]****。 如果 **[屬性]** 選項已停用，請確認您已使用系統管理權限來啟動 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 。  
  
    4.  選取 **[啟用 ActiveX 用戶端列印控制項的下載**]。  
  
    5.  按一下 [確定]  。  
  
-   針對 **SharePoint 模式報表伺服器**：  
  
    1.  在 SharePoint 管理中心內，按一下 **[應用程式管理]**。  
  
    2.  按一下 **[管理服務應用程式]**。  
  
    3.  按一下 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的名稱，然後按一下 SharePoint 功能區中的 **[管理]** 。  
  
    4.  按一下 **[系統設定]**。  
  
    5.  選取 **[啟用用戶端列印]**。 **[啟用用戶端列印]** 選項位於靠近頁面底部的位置。  
  
    6.  按一下 [確定]  。  
  
-   撰寫腳本或程式碼，將報表伺服器系統屬性**EnableClientPrinting**設定為`false.`  
  
 下列範例指令碼說明停用用戶端列印功能的方法之一。 編譯後執行下列 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 程式碼，將 **EnableClientPrinting** 屬性設定為 **False**。 執行程式碼之後，請重新啟動 IIS。  
  
### <a name="sample-script"></a>範例指令碼  
  
```  
Imports System  
Imports System.Web.Services.Protocols  
Class Sample  
   Public Shared Sub Main()  
Dim rs As New ReportingService()  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
        Dim props(0) As [Property]  
        Dim setProp As New [Property]  
        setProp.Name = "EnableClientPrinting"  
        setProp.Value = "False"   
        props(0) = setProp  
        Try  
            rs.SetSystemProperties(props)  
        Catch ex As System.Web.Services.Protocols.SoapException  
            Console.Write(ex.Detail.InnerXml)  
        Catch e as Exception  
            Console.Write(e.Message)  
        End Try  
    End Sub 'Main  
End Class 'Sample  
```  
  
  
