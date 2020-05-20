---
title: 執行通訊錄範例應用程式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 3a2644e9-d634-4ae6-a5b7-13fb7b317ec7
author: rothja
ms.author: jroth
ms.openlocfilehash: e3a2c971f952a7c3f13b058bb3937201d323746d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758984"
---
# <a name="running-the-address-book-sample-application"></a>執行通訊錄應用程式範例
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 若要執行通訊錄應用程式，請遵循此步驟。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
### <a name="to-run-this-application"></a>執行此應用程式  
  
1.  請確定 Microsoft SQL Server 正在執行。 按一下 [**開始**]，指向 [**程式**]，指向 [ **Microsoft SQL Server 7.0**]，然後按一下 [ **Service Manager**]。 如果白色圓圈中有綠色箭號，表示 SQL Server 正在執行。 如果不是（白色圓圈中會有紅色方塊），請按一下 [開始] **/[繼續**]。  
  
2.  在 Microsoft Internet Explorer 4.0 或更新版本中，輸入下列位址：  
  
     **HTTPs://** *web*伺服器 **/RDS/AddressBook/AddrBook.asp**  
  
     其中 *，* 伺服器名稱是安裝 RDS 伺服器元件的 Web 服務器名稱。  
  
3.  接著，您可以在通訊錄範例應用程式中嘗試各種案例，例如根據電子郵件名稱搜尋人員、列出所有標題為「程式經理」的人員，或編輯現有的記錄。 按一下 [**尋找**] 以填滿所有可用名稱的資料格。  
  
## <a name="see-also"></a>另請參閱  
 [通訊錄資料繫結物件](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)




