---
title: 執行通訊錄範例應用程式 |Microsoft 文件
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
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 3a2644e9-d634-4ae6-a5b7-13fb7b317ec7
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 958ab049bae05f1209d51410d49cab9bdd325562
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="running-the-address-book-sample-application"></a>執行通訊錄範例應用程式
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 若要執行通訊錄應用程式，請遵循此程序。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
### <a name="to-run-this-application"></a>若要執行此應用程式  
  
1.  請確定 Microsoft SQL Server 正在執行。 按一下**啟動**，指向 **程式**，指向  **Microsoft SQL Server 7.0**，然後按一下  **Service Manager**。 如果白色圓形中有綠色箭號，SQL Server 正在執行。 如果不是 （會有紅色方形白色圓形中），按一下 **啟動/繼續**。  
  
2.  在 Microsoft Internet Explorer 4.0 或更新版本中，輸入下列位址：  
  
     **http://** *webserver* **/RDS/AddressBook/AddrBook.asp**  
  
     其中*webserver* RDS 伺服器元件的安裝位置的 Web 伺服器的名稱。  
  
3.  您可以再嘗試通訊錄範例應用程式中的各種案例，例如搜尋人員根據他或她列出所有標題為 「 程式經理 」 的人員的電子郵件名稱或編輯現有記錄。 按一下**尋找**資料方格中填入所有可用的名稱。  
  
## <a name="see-also"></a>另請參閱  
 [通訊錄資料繫結物件](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)




