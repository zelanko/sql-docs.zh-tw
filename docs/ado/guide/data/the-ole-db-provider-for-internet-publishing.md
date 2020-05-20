---
title: 網際網路發佈的 OLE DB 提供者 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 813b7e108f375fdbd22ba10761678907aea912f6
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759054"
---
# <a name="the-ole-db-provider-for-internet-publishing"></a>適用於網際網路發佈的 OLE DB 提供者
ADO[記錄](../../../ado/reference/ado-api/record-object-ado.md)和[串流](../../../ado/reference/ado-api/stream-object-ado.md)物件可與 Microsoft OLE DB Provider For Internet 發行（網際網路發佈提供者）搭配使用，以存取和操作 microsoft FrontPage 所提供的資源，例如 Web 資料夾或檔案。 使用 ADO，您可以將**記錄**、**資料流程**或[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的來源指定為 URL。 然後您可以上傳、下載、移動、複製和刪除資源，或直接操作資源屬性。  
  
 如需搭配網際網路發行提供者使用**記錄**和**串流**的範例程式碼，請參閱[網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)。  
  
 網際網路發佈提供者是與 Microsoft Windows 2000 一起安裝的。 舊版的網際網路發行提供者也適用于 Microsoft Office 2000 和 Microsoft Internet Explorer 5.0。  
  
 有三種方式可將 ADO 連接到網際網路發佈提供者：  
  
-   在連接字串中指定 "URL ="。 例如：  
  
    ```  
    objConn.Open "URL=https://servername"  
    ```  
  
-   針對連接字串的*Provider*關鍵字指定 Msdaipp。 例如：  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=https://servername"  
    ```  
  
-   針對[Connection](../../../ado/reference/ado-api/connection-object-ado.md)物件的[Provider](../../../ado/reference/ado-api/provider-property-ado.md)屬性指定 Msdaipp。 例如：  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "https://servername"  
    ```  
  
> [!NOTE]
>  如果 Msdaipp 是*以提供者連接字串*關鍵字或**提供**者屬性明確指定為提供者的值，您就不能在連接字串中使用 "URL ="。 如果您這樣做，將會發生錯誤。 相反地，只需指定 URL，如先前所示。  
  
 如需有關網際網路發佈提供者的詳細資訊，請參閱[適用于網際網路發佈的 Microsoft OLE DB 提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)，或已安裝用於網際網路發行之 OLE DB 提供者的來源應用程式所提供的提供者檔： Windows 2000、Office 2000 或 internet Explorer 5.0。
