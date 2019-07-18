---
title: Reporting Services 傳遞延伸模組設定 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- XML Web service [Reporting Services], delivery extension settings
- Report Server Web service, delivery extension settings
- delivery [Reporting Services]
- network share delivery [Reporting Services]
- file share delivery [Reporting Services]
- e-mail [Reporting Services]
- mailing reports [Reporting Services]
- sharing reports
- extensions [Reporting Services], delivery
- mail [Reporting Services]
- Web service [Reporting Services], delivery extension settings
ms.assetid: 68c31a85-261c-4ec4-b8df-1f9842b46f8a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d356bc1cb981479de8a4b1baa3bdaaf45b6145ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63260753"
---
# <a name="reporting-services-delivery-extension-settings"></a>Reporting Services 傳遞延伸模組設定
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 包括電子郵件傳遞延伸模組以及檔案共用傳遞延伸模組。 電子郵件傳遞提供一個透過電子郵件傳送報表給個別使用者或群組的方法。 檔案共用傳遞可讓您將轉譯的報表自動傳送給網路上的共用。 您可以使用其中一個支援的傳遞延伸模組搭配標準訂閱或資料驅動訂閱來傳送。 每當您呼叫 <xref:ReportService2010.ReportingService2010.CreateSubscription%2A>、<xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>、<xref:ReportService2010.ReportingService2010.SetSubscriptionProperties%2A> 和 <xref:ReportService2010.ReportingService2010.SetDataDrivenSubscriptionProperties%2A> 方法時，會傳遞特屬傳遞延伸模組類型的傳遞設定。 若要以程式設計的方式擷取傳遞設定清單，請使用 <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A> 方法。  
  
> [!NOTE]  
>  傳遞延伸模組設定需要區分大小寫。  
  
## <a name="e-mail-delivery-settings"></a>電子郵件傳遞設定  
 下表針對使用報表伺服器電子郵件的訂閱列出電子郵件傳遞設定。  
  
|設定|值|  
|-------------|-----------|  
|**收件人**|出現在電子郵件訊息的 `To` 之電子郵件地址。 分號會分隔多個電子郵件地址。 必要。|  
|**CC**|出現在電子郵件訊息的 `Cc` 之電子郵件地址。 分號會分隔多個電子郵件地址。 選擇性。|  
|**密件副本**|出現在電子郵件訊息的 `Bcc` 之電子郵件地址。 分號會分隔多個電子郵件地址。 選擇性。|  
|**ReplyTo**|出現在電子郵件訊息的 `Reply-To` 標頭之電子郵件地址。 值必須是單一電子郵件地址。 選擇性。|  
|`IncludeReport`|指出在電子郵件傳遞中是否包括報表的值。 `true` 的值指出在電子郵件訊息的本文中所傳遞的報表。|  
|**RenderFormat**|要用以產生轉譯報表的轉譯延伸模組名稱。 名稱必須對應至報表伺服器上安裝的其中一個可見的轉譯延伸模組。 如果將 `IncludeReport` 設定為 `true` 的值，則這個值是必要的。|  
|**優先權**|傳送電子郵件訊息的優先權。 有效值為 `LOW`、`NORMAL` 及 `HIGH`。 預設值是 `NORMAL`。|  
|**主旨**|電子郵件訊息主旨中的文字。|  
|**註解**|文字包括在電子郵件訊息的本文中。|  
|**IncludeLink**|指出在電子郵件本文中是否包括報表連結的值。|  
  
## <a name="file-share-delivery-settings"></a>檔案共用傳遞設定  
 下表列出訂閱的檔案共用傳遞設定。  
  
|設定|值|  
|-------------|-----------|  
|**FILENAME**|儲存到磁碟的檔案名稱。|  
|**FILEEXTN**|指出轉譯報表是否包括副檔名。 值是 `true` 或是 `false`。|  
|**PATH**|儲存報表的資料夾路徑或是 UNC 檔案共用路徑。|  
|**RENDER_FORMAT**|儲存到磁碟的報表格式。|  
|**USERNAME**|存取網路資源或磁碟所需的使用者名稱。|  
|**PASSWORD**|存取網路資源或磁碟所需的密碼。|  
|**WRITEMODE**|存取磁碟時使用的寫入模式。 有效值為 `None`、`Overwrite` 及 `AutoIncrement`。|  
  
## <a name="see-also"></a>另請參閱  
 [技術參考 &#40;SSRS&#41;](../../technical-reference-ssrs.md)   
 [使用 Web 服務和.NET Framework 建置應用程式](building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
