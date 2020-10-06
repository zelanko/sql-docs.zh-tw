---
description: 執行通訊錄應用程式範例
title: 執行通訊錄範例應用程式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 85d9dbf43107af7504241af825b5b21c38139e3b
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91723051"
---
# <a name="running-the-address-book-sample-application"></a>執行通訊錄應用程式範例
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
 若要執行通訊錄應用程式，請遵循此程式。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
### <a name="to-run-this-application"></a>若要執行此應用程式  
  
1.  確定 Microsoft SQL Server 正在執行。 按一下 [ **開始**]，指向 [ **程式**]，指向 [ **Microsoft SQL Server 7.0**]，然後按一下 [ **Service Manager**]。 如果白色圓圈中有綠色箭號，表示 SQL Server 正在執行。 如果未 (，白色圓圈中將會有紅色方形) ，請按一下 [ **開始]/[繼續**]。  
  
2.  在 Microsoft Internet Explorer 4.0 或更新版本中，輸入下列位址：  
  
     **HTTPs://** *web*伺服器 **/RDS/AddressBook/AddrBook.asp**  
  
     其中 *web 伺服器是安裝* RDS 伺服器元件的網頁伺服器名稱。  
  
3.  然後，您可以嘗試通訊錄範例應用程式中的各種案例，例如根據他或她的電子郵件名稱搜尋人員、列出所有標題為 [Program Manager] 的人員，或編輯現有的記錄。 按一下 [ **尋找** ]，以所有可用的名稱填滿資料格。  
  
## <a name="see-also"></a>另請參閱  
 [通訊錄資料繫結物件](./address-book-data-binding-object.md)