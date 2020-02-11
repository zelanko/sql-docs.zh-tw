---
title: 適用于網際網路發佈的 Microsoft OLE DB 提供者 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
- Internet Publishing provider [ADO]
ms.assetid: 66a208d9-b580-4655-a41e-1d36e5b5bfca
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 19d719ddb4e5a2f7851a1d12dc4abe69069a354f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926757"
---
# <a name="microsoft-ole-db-provider-for-internet-publishing-overview"></a>適用于網際網路發佈的 Microsoft OLE DB 提供者總覽
適用于網際網路發佈的 Microsoft OLE DB 提供者可讓 ADO 存取由 Microsoft FrontPage 或 Microsoft Internet information Server 提供的資源。 資源包括 web 來源檔案，例如 HTML 檔案或 Windows 2000 web 資料夾。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到這個提供者，請將[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性的*provider*引數設定為：

```vb
MSDAIPP.DSO
```

 這個值也可以使用[Provider](../../../ado/reference/ado-api/provider-property-ado.md)屬性來設定或讀取。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串為：

```vb
"Provider=MSDAIPP.DSO;Data Source=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 -或-

```vb
"URL=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 此字串包含下列關鍵字：

|關鍵字|描述|
|-------------|-----------------|
|**提供者**|指定網際網路發行的 OLE DB 提供者。|
|**資料來源**-或- **URL**|指定在 Web 資料夾中發佈之檔案或目錄的 URL。|
|**使用者識別碼**|指定使用者名稱。|
|**密碼**|指定使用者密碼。|

> [!NOTE]
>  如果您要連接到支援 Windows 驗證的資料來源提供者，您應該在連接字串中指定**Trusted_Connection = yes**或**整合式安全性 = SSPI** ，而不是使用者識別碼和密碼資訊。

 如果您將連接字串中 "URL =" 的*ResourceURL*值設定為不正確值，則網際網路發佈提供者預設會引發一個對話方塊，提示您輸入有效的值。 這對應用程式仲介層中的元件而言是不想要的行為，因為它會暫停程式執行，直到清除對話方塊，而且用戶端似乎已凍結，因為它尚未收到來自元件的回應。

> [!NOTE]
>  如果 MSDAIPP，則為。DSO 是*以提供者連接字串*關鍵字或**提供**者屬性明確指定為提供者的值，您不能在連接字串中使用 "URL ="。 如果您這樣做，將會發生錯誤。 相反地，只需指定 URL，如搭配[使用 ADO 與 OLE DB 提供者進行網際網路發佈](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)主題中所示。

## <a name="see-also"></a>另請參閱
 [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)網際網路[發行的 OLE DB 提供者](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)
