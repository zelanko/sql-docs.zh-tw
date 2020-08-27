---
description: 適用於網際網路發佈的 OLE DB 提供者
title: 適用于網際網路發佈的 OLE DB 提供者 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7556d3857142a4762fd411f5175a38c2e4d58cf3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979359"
---
# <a name="the-ole-db-provider-for-internet-publishing"></a>適用於網際網路發佈的 OLE DB 提供者
ADO [Record](../../../ado/reference/ado-api/record-object-ado.md) 和 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 物件可搭配 Microsoft OLE DB Provider For Internet 發佈 (網際網路發佈提供者) 存取及操作資源，例如，Web 資料夾或 Microsoft FrontPage 提供的檔案。 您可以使用 ADO 將 **記錄**、 **資料流程**或 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 的來源指定為 URL。 然後，您可以上傳、下載、移動、複製和刪除資源，或直接操作資源屬性。  
  
 如需使用 **記錄** 和 **串流** 處理網際網路發佈提供者的程式碼範例，請參閱 [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)。  
  
 網際網路發佈提供者與 Microsoft Windows 2000 一起安裝。 Microsoft Office 2000 和 Microsoft Internet Explorer 5.0 也提供舊版的網際網路發佈提供者。  
  
 有三種方式可以將 ADO 連接至網際網路發佈提供者：  
  
-   在連接字串中指定 "URL ="。 例如：  
  
    ```  
    objConn.Open "URL=https://servername"  
    ```  
  
-   針對連接字串的 *Provider* 關鍵字指定 msdaipp.dll。 例如：  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=https://servername"  
    ```  
  
-   針對[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件的[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性指定 msdaipp.dll。 例如：  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "https://servername"  
    ```  
  
> [!NOTE]
>  如果 Msdaipp.dll 已明確指定為提供者的值（使用 *提供者* 連接字串關鍵字或 **提供者** 屬性），則您無法在連接字串中使用 "URL ="。 如果您這樣做，將會發生錯誤。 相反地，只要指定 URL 即可，如先前所示。  
  
 如需更多有關網際網路發佈提供者的詳細資訊，請參閱 [Microsoft OLE DB Provider For Internet 發佈](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)，或是隨來源應用程式提供的提供者檔，其中已安裝適用于網際網路發佈的 OLE DB 提供者： Windows 2000、Office 2000 或 Internet Explorer 5.0。
