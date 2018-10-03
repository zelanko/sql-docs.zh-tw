---
title: 適用於網際網路發佈的 Microsoft OLE DB 提供者 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
- Internet Publishing provider [ADO]
ms.assetid: 66a208d9-b580-4655-a41e-1d36e5b5bfca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 56e780efde72007d9ed4f1b701cde220a0f9be4e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47688116"
---
# <a name="microsoft-ole-db-provider-for-internet-publishing-overview"></a>Microsoft OLE DB Provider for Internet 發行等概觀
Microsoft OLE DB Provider for Internet Publishing 會將 ADO 可以存取由 Microsoft FrontPage 或 Microsoft Internet Information Server 的資源。 資源包括 web 來源檔案，例如 HTML 檔案或 Windows 2000 web 資料夾。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到此提供者，將*提供者*引數[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性：

```
MSDAIPP.DSO
```

 此值也可以設定或使用讀取[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串是：

```
"Provider=MSDAIPP.DSO;Data Source=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 -或-

```
"URL=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 字串是由這些關鍵字所組成：

|關鍵字|描述|
|-------------|-----------------|
|**提供者**|指定適用於網際網路發佈的 OLE DB 提供者。|
|**資料來源**-或- **URL**|指定的檔案或目錄已發佈 Web 資料夾中的 URL。|
|**使用者識別碼**|指定使用者名稱。|
|**密碼**|指定使用者密碼。|

> [!NOTE]
>  如果您要連接到資料來源提供者支援 Windows 驗證，您應該指定**Trusted_Connection = yes**或是**Integrated Security = SSPI**而非使用者 ID 和密碼連接字串中的資訊。

 如果您設定*ResourceURL*值從"URL ="在連接字串中無效的值，預設的網際網路發行提供者引發一個對話方塊，提示您輸入有效的值。 因為它會暫止程式執行，直到清除對話方塊中，而且用戶端似乎會凍結，因為它未收到回應的元件，這會是中介層應用程式元件的非預期行為。

> [!NOTE]
>  如果 MSDAIPP。DSO 明確指定的提供者，不論是使用值為*提供者*連接字串關鍵字，或有**提供者**屬性，您無法使用"URL ="連接字串中。 如果您這樣做，會發生錯誤。 本主題中所示相反地，只要指定 URL[使用的 ADO 與 OLE DB Provider for Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)。

## <a name="see-also"></a>另請參閱
 [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)[網際網路發佈的 OLE DB 提供者](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)
