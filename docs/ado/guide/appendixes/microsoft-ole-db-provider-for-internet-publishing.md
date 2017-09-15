---
title: "Microsoft OLE DB Provider for Internet 發行 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
- Internet Publishing provider [ADO]
ms.assetid: 66a208d9-b580-4655-a41e-1d36e5b5bfca
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d466123e7330eb599847225d2b108ec7f80d9ea9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-ole-db-provider-for-internet-publishing-overview"></a>Microsoft OLE DB Provider for Internet 發行概觀
Microsoft OLE DB Provider for Internet Publishing 可讓 ADO 存取資源，由 Microsoft FrontPage 或 Microsoft Internet Information Server。 資源包括 web 來源檔案，例如 HTML 檔案、 或 Windows 2000 web 資料夾。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到此提供者，設定*提供者*引數的[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性：

```
MSDAIPP.DSO
```

 這個值也可以設定或讀取使用[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串是：

```
"Provider=MSDAIPP.DSO;Data Source=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 -或-

```
"URL=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 字串，包含這些關鍵字：

|關鍵字|Description|
|-------------|-----------------|
|**提供者**|指定網際網路發行的 OLE DB 提供者。|
|**資料來源**-或- **URL**|指定的檔案或目錄已發佈的 Web 資料夾中的 URL。|
|**使用者識別碼**|指定使用者名稱。|
|**密碼**|指定的使用者密碼。|

> [!NOTE]
>  如果您要連接至資料來源提供者支援 Windows 驗證，您應該指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是使用者識別碼和密碼連接字串中的資訊。

 如果您設定*ResourceURL*值從"URL ="在連接字串中無效的值，預設網際網路發行提供者會引發一個對話方塊，提示您輸入有效的值。 這是不必要的行為，應用程式的中介層中的元件，因為它會暫止程式執行，直到清除對話方塊中，而且用戶端似乎凍結，因為它未收到回應的元件。

> [!NOTE]
>  如果 MSDAIPP。做為值的提供者，不論是透過明確指定 DSO*提供者*連接字串關鍵字或**提供者**屬性，您無法使用 」 URL ="連接字串中。 如果您這樣做，就會發生錯誤。 本主題中所示相反地，只要指定 URL[使用 ADO 與 OLE DB Provider for Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)。

## <a name="see-also"></a>另請參閱
 [發佈案例的網際網路](../../../ado/guide/data/internet-publishing-scenario.md)[網際網路發行的 OLE DB 提供者](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)

