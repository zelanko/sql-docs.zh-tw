---
title: OLE DB Provider for Internet 發行 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
ms.assetid: 4869aafa-7401-4ce1-93ce-45406a60274f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c3dfd95a9df4e67effa659e3d76d92ce1927d778
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="the-ole-db-provider-for-internet-publishing"></a>OLE DB Provider for Internet 發行
ADO[記錄](../../../ado/reference/ado-api/record-object-ado.md)和[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件可用於搭配 Microsoft OLE DB Provider for Internet Publishing （網際網路發行的提供者） 存取及管理資源，例如 Web 資料夾或檔案由 Microsoft FrontPage。 ADO 中，您可以指定的來源**記錄**，**資料流**，或[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)是 url。 您可以然後上傳、 下載、 移動、 複製和刪除資源，或直接管理 資源內容。  
  
 如需範例程式碼，會使用**記錄**和**資料流**網際網路發行提供者使用，請參閱[網際網路發行案例](../../../ado/guide/data/internet-publishing-scenario.md)。  
  
 網際網路發行的提供者會隨 Microsoft Windows 2000。 舊版的網際網路發行的提供者也會提供與 Microsoft Office 2000 和 Microsoft Internet Explorer 5.0 的。  
  
 有三種方式可連接到網際網路發行的提供者的 ADO:  
  
-   指定 「 URL ="連接字串中。 例如：  
  
    ```  
    objConn.Open "URL=http://servername"  
    ```  
  
-   指定針對 Msdaipp.dso*提供者*的連接字串關鍵字。 例如：  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=http://servername"  
    ```  
  
-   指定針對 Msdaipp.dso[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。 例如：  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "http://servername"  
    ```  
  
> [!NOTE]
>  如果做為值的提供者，不論是透過明確指定 Msdaipp.dso*提供者*連接字串關鍵字或**提供者**屬性，您無法使用 」 URL ="連接字串中。 如果您這樣做，就會發生錯誤。 相反地，只要指定的 URL 前面所示。  
  
 更具體的網際網路發行的提供者相關的詳細資訊，請參閱[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)，或提供者文件的來源應用程式提供 OLE DB 提供者已安裝 Internet Publishing: Windows 2000、 Office 2000 或 Internet Explorer 5.0。
