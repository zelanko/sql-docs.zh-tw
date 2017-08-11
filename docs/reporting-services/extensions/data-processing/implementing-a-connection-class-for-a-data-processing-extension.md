---
title: "資料處理延伸模組實作 Connection 類別 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- connections [Reporting Services], data processing extensions
- Connection class
- data processing extensions [Reporting Services], connections
ms.assetid: 7047d29e-a2c9-4e6f-ad02-635851a38ed7
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 19f059c0041cc9effc48e0db9c4b5ef1a504d020
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="implementing-a-connection-class-for-a-data-processing-extension"></a>為資料處理延伸模組實作 Connection 類別
  **連接**物件代表資料庫連結或是類似的資源，而且是使用者的起點[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]資料處理延伸模組。 它代表連線到資料庫伺服器，但類似的行為與任何實體可公開為**連接**。  
  
 若要實作**連接**物件，請建立可實作<xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>並選擇性地實作<xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>。  
  
 在您的實作中，您必須確保在執行命令之前先建立和開啟連接。 請確保實作要求用戶端明確地開啟和關閉連接，而不是讓您的實作隱含地為用戶端開啟和關閉連接。 在取得連接時執行您的安全性檢查。 在 [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] 資料處理延伸模組中需要其他類別的現有連接，將可確保在與資料來源搭配使用時永遠執行安全性檢查。  
  
 所需連接的屬性是以連接字串來表示。 強烈建議 [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] 資料處理延伸模組使用由 OLE DB 定義的熟悉名稱/值組系統來支援 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection.ConnectionString%2A> 屬性。  
  
> [!NOTE]  
>  **連接**物件通常是大量的資源來取得，所以您可能會想要考慮共用連接或其他技術來減少這種情況。  
  
 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> 繼承自 <xref:Microsoft.ReportingServices.Interfaces.IExtension>。 您必須將 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 介面實作為連接類別實作的一部分。 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 介面允許類別實作當地語系化的延伸模組名稱，並處理在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 組態檔中儲存的延伸模組特定組態資訊。  
  
 您**連接**物件包含<xref:Microsoft.ReportingServices.Interfaces.IExtension.LocalizedName%2A>屬性透過其實作<xref:Microsoft.ReportingServices.Interfaces.IExtension>。 強烈建議 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組支援 <xref:Microsoft.ReportingServices.Interfaces.IExtension.LocalizedName%2A> 屬性，這樣使用者便會在使用者介面遇到熟悉且當地語系化的延伸模組名稱，例如報表管理員。  
  
 <xref:Microsoft.ReportingServices.Interfaces.IExtension>也可讓您**連接**物件擷取和處理儲存在 RSReportServer.config 檔案中的自訂組態資料。 如需有關處理自訂組態資料的詳細資訊，請參閱＜<xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A>＞方法。  
  
 當未卸載其餘的資料處理延伸模組類別時，實作 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 的類別不會從記憶體卸載。 因為這個緣故，您可以使用您**延伸**類別來儲存跨連接的狀態資訊，或可以快取的資料儲存在記憶體中。 您**延伸**類別仍然會在記憶體中，只要報表伺服器正在執行。  
  
 您可以擴充您**連接**類別，以包含支援的認證在[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]藉由實作<xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>。 當您實作<xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.IntegratedSecurity%2A>， <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.UserName%2A>，和<xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.Password%2A>屬性<xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>介面，啟用**整合式安全性**核取方塊和**Username**和**密碼**文字方塊的**資料來源**對話方塊在報表設計師中的。 這允許報表設計師儲存和擷取支援驗證的資料來源之認證。 會將認證安全地儲存並在預覽模式中轉譯報表時使用。  
  
> [!NOTE]  
>  若要隱含實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>，您必須實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> 與 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 介面的成員。  
>   
>  如需範例**連接**類別的實作，請參閱[SQL Server Reporting Services 產品範例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [實作資料處理延伸模組](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
