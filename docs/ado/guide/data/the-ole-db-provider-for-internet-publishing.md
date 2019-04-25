---
title: 適用於網際網路發佈的 OLE DB 提供者 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
ms.assetid: 4869aafa-7401-4ce1-93ce-45406a60274f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3acf5ed94993d50c3c81813cd9ea09db2c231a08
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472207"
---
# <a name="the-ole-db-provider-for-internet-publishing"></a>適用於網際網路發佈的 OLE DB 提供者
ADO[記錄](../../../ado/reference/ado-api/record-object-ado.md)並[Stream](../../../ado/reference/ado-api/stream-object-ado.md)物件可用 Microsoft OLE DB provider for Internet Publishing （網際網路發行的提供者） 來存取及管理資源，例如 Web 資料夾或檔案由 Microsoft FrontPage。 ADO 中，您可以指定的來源**記錄**， **Stream**，或[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)是 URL。 您可以接著上傳、 下載、 移動、 複製和刪除資源，或直接管理資源的屬性。  
  
 比方說使用的程式碼**記錄**並**串流**網際網路發佈提供者，請參閱[網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)。  
  
 網際網路發佈提供者會隨 Microsoft Windows 2000。 較早版本的網際網路發行提供者也有 Microsoft Office 2000 與 Microsoft Internet Explorer 5.0。  
  
 有三種方式可以連線到網際網路發佈提供者的 ADO:  
  
-   指定"URL ="連接字串中。 例如：  
  
    ```  
    objConn.Open "URL=https://servername"  
    ```  
  
-   指定針對 Msdaipp.dso*提供者*的連接字串關鍵字。 例如：  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=https://servername"  
    ```  
  
-   指定針對 Msdaipp.dso[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件。 例如：  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "https://servername"  
    ```  
  
> [!NOTE]
>  如果 Msdaipp.dso 明確指定的提供者，不論是使用值為*提供者*連接字串關鍵字或**提供者**屬性，您無法使用"URL ="連接字串中。 如果您這樣做，會發生錯誤。 相反地，只要指定 URL 稍早所示。  
  
 更具體的網際網路發行提供者的詳細資訊，請參閱[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)，或提供者文件，與來源應用程式提供 OLE DB Provider for已安裝 Internet Publishing:Windows 2000、 Office 2000 或 Internet Explorer 5.0。
