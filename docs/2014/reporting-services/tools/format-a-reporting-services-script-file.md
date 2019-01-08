---
title: 格式化 Reporting Services 指令碼檔案 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services], formats
- formats [Reporting Services], script files
ms.assetid: 85a207dd-4e0f-4d40-a41e-0c75f65d719c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: bd33fa4ddfe9f90d7041cf5f6d5b0a47da757a59
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53350764"
---
# <a name="format-a-reporting-services-script-file"></a>格式化 Reporting Services 指令碼檔案
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 指令碼是針對 Web Service Description Language (WSDL) 內建 Proxy 撰寫的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET 程式碼檔案，其中會定義 Reporting Services SOAP API。 指令碼檔案會儲存為 Unicode 或 UTF-8 文字檔，且其副檔名為 .rss。  
  
 指令碼檔案的用途如何 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 模組，而且可以包含使用者自訂程序和模組層次的變數。 若要讓指令碼檔案自動執行，則必須包含 Main 程序。 Main 程序是指令碼檔案執行時存取的第一個程序。 Main 是您可以加入 Web 服務作業並執行使用者自訂子程序的地方。 下列程式碼會建立 Main 程序：  
  
```  
Public Sub Main()  
    ' Your code goes here.  
End Sub  
```  
  
 指令碼環境會自動連接到報表伺服器、建立 Web Proxy 類別，然後產生 Web 服務 Proxy 物件的參考變數 (*rs*)。 您所建立的個別陳述式僅需要參考 *rs* 模組層次的變數，就能夠執行 Web 服務程式庫中提供的任何 Web 服務作業。 下列 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 程式碼會從指令碼檔案內，呼叫 Web 服務的 <xref:ReportService2010.ReportingService2010.ListChildren%2A> 方法：  
  
```  
Public Sub Main()  
    Dim items() As CatalogItem  
    items = rs.ListChildren("/", True)  
  
    Dim item As CatalogItem  
    For Each item In items  
        Console.WriteLine(item.Name)  
    Next item  
End Sub   
```  
  
> [!IMPORTANT]  
>  使用者認證會由指令碼環境所管理，並藉由使用 RS.exe，透過命令提示字元引數傳遞。 您可以使用 *rs* 變數來設定 Web 服務的驗證，但是建議您使用指令碼環境。 您不需要在指令碼檔案本身，驗證 Web 服務。 如需有關驗證指令碼環境的詳細資訊，請參閱 [RS.exe 公用程式 &#40;SSRS&#41;](rs-exe-utility-ssrs.md)。  
  
 您沒有宣告指令碼檔案內的命名空間。 指令碼環境提供數個實用[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]命名空間供您：**System.Web.Services**， **System.Web.Services.Protocols**， **System.Xml**，和**System.IO**。  
  
 如需指令碼範例，請參閱 [SQL Server Reporting Services 產品範例](https://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另請參閱  
 [報表伺服器 Web 服務](../report-server-web-service/report-server-web-service.md)   
 [技術參考 &#40;SSRS&#41;](../technical-reference-ssrs.md)   
 [RS.exe 公用程式 &#40;SSRS&#41;](rs-exe-utility-ssrs.md)  
  
  
