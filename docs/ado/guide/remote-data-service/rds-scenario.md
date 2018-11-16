---
title: RDS 案例 |Microsoft Docs
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
ms.assetid: a7dcad87-aaf0-4b02-9660-472f8469761c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e936b6b68a67c1616a00d38f6d84776d44ef327
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/12/2018
ms.locfileid: "51559431"
---
# <a name="rds-scenario"></a>RDS 案例
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 通訊錄應用程式會示範如何使用遠端資料服務 (RDS) 來建置簡單的資料感知的 Web 應用程式的案例 — 企業線上通訊錄。 此案例適用於 Microsoft Visual Basic Scripting Edition (VBScript) COM 程式設計人員想要了解如何使用資料感知的 ActiveX 控制項有了 RDS，且較有經驗的軟體開發人員想要建置以資料為中心的 Web 應用程式。  
  
 此案例假設您知道如何使用 ActiveX 控制項的基本 HTML 配置標記、 使用 DHTML 資料繫結技術和程式。  
  
 如果您已安裝 SDK，就可以找到通訊錄範例應用程式的完整原始程式碼位於 samples\dataaccess\rds\AddressBook\AddressBook.asp SDK 目錄中。 若要檢視的通訊錄案例，請在 Internet Explorer 4.0 或更新版本中，輸入**https://*webserver*/RDS/AddressBook/AddressBook.asp**其中*webserver*名稱提供給 Windows NT 4.0 或 Windows 2000 Web 伺服器電腦正在執行 Internet Information Services (IIS) 和 ASP。  
  
## <a name="introduction-to-address-book"></a>簡介通訊錄  
 通訊錄範例應用程式提供一個簡單線上通訊錄，您可以使用透過內部網路發佈的可搜尋的目錄。 通訊錄經過設計，因此使用者可以要求員工的相關資訊的一或多個欄位中輸入搜尋字串。 若要顯示的遠端資料服務的基本功能，範例應用程式刻意保持小型、 最小數目的物件和搜尋欄位。  
  
 應用程式介面是由下列部分所組成：  
  
-   非視覺**rds。DataControl**可由用戶端來連接到資料庫的資料繫結物件。  
  
-   做為輸入欄位，以便員工屬性的 HTML 文字方塊中的搜尋條件。  
  
-   HTML 命令按鈕，來建立查詢，會清除搜尋欄位、 更新資料庫中的員工資訊、 取消暫止的變更，和瀏覽的方格中顯示的資料列的資料。  
  
-   DHTML 資料繫結至顯示資料從查詢傳回的比對後端資料庫 (透過**rds。DataControl**資料繫結物件) 資料表中。  
  
-   連線到每個先前所述的項目並允許它們能夠互動的 VBScript 常式。 VBScript 程式碼也會用來初始化**rds。DataControl**物件，並動態建立 HTML 資料表的名稱中的 資料行標題**rds。DataControl**資料錄集欄位。  
  
 遵循步驟的連結，來設定和執行的案例，以及深入了解案例的運作方式的步驟。  
  
 此案例包含下列主題。  
  
-   [通訊錄應用程式的系統需求](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)  
  
-   [執行通訊錄 SQL 指令碼](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)  
  
-   [執行通訊錄範例應用程式](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)  
  
-   [通訊錄資料繫結物件](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)  
  
-   [通訊錄命令按鈕](../../../ado/guide/remote-data-service/address-book-command-buttons.md)  
  
-   [通訊錄導覽按鈕](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>另請參閱  
 [通訊錄應用程式的系統需求](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)   
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)


