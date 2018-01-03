---
title: "RDS 案例 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: a7dcad87-aaf0-4b02-9660-472f8469761c
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 10c9ee41428ab7a43beae2269060618f7d6e296b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="rds-scenario"></a>RDS 案例
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 通訊錄應用程式會示範如何使用遠端資料服務 (RDS) 來建立簡單資料感知的 Web 應用程式的案例 — 公司線上通訊錄。 此案例適用於 Microsoft Visual Basic Scripting Edition (VBScript) 和 COM 的程式設計人員想要了解如何使用資料感知的 ActiveX 控制項與 RDS，以及較有經驗的軟體開發人員想要建置以資料為中心的 Web 應用程式。  
  
 此案例假設您知道如何使用 ActiveX 控制項的基本 HTML 配置標記、 使用 DHTML 資料繫結技術和程式。  
  
 如果您已經安裝 SDK，可以在 samples\dataaccess\rds\AddressBook\AddressBook.asp SDK 目錄中找到通訊錄範例應用程式的完整原始程式碼。 若要檢視的通訊錄案例，請在 Internet Explorer 4.0 或更新版本中，輸入 **http://*webserver*/RDS/AddressBook/AddressBook.asp** 其中*webserver*名稱提供給 Windows NT 4.0 或 Windows 2000 Web 伺服器電腦正在執行 Internet Information Services (IIS) 和 ASP。  
  
## <a name="introduction-to-address-book"></a>Introduction to 通訊錄  
 通訊錄範例應用程式提供一個簡單線上通訊錄，您可以使用內部網路上發佈可搜尋的目錄。 通訊錄的設計，讓使用者能夠輸入搜尋字串中，要求有關員工資訊的一或多個欄位。 若要顯示的遠端資料服務的基本功能，範例應用程式是刻意保持在最少，使用物件和搜尋欄位的最小數目。  
  
 應用程式介面是由下列部分所組成：  
  
-   非 visual **.RDSDataControl**用戶端用來連接到資料庫的資料繫結物件。  
  
-   做為輸入的欄位，員工屬性搜尋準則的 HTML 文字方塊。  
  
-   HTML 命令按鈕，建立查詢，清除搜尋欄位，請更新資料庫中 「 員工 」 資訊、 取消暫止的變更，並瀏覽的方格中顯示的資料列。  
  
-   DHTML 資料繫結來顯示資料查詢所傳回的比對後端資料庫 (透過**.RDSDataControl**資料繫結物件) 資料表中。  
  
-   VBScript 常式連接每個先前所述的元素，並允許它們互動。 VBScript 程式碼也會用來初始化**.RDSDataControl**物件，並以動態方式在 HTML 表格的名稱建立資料行標題**.RDSDataControl**資料錄集欄位。  
  
 請從步驟的連結，步驟來設定和執行案例，以及深入了解案例的運作方式。  
  
 這個案例包含下列主題。  
  
-   [通訊錄應用程式的系統需求](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)  
  
-   [執行通訊錄 SQL 指令碼](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)  
  
-   [執行通訊錄範例應用程式](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)  
  
-   [通訊錄資料繫結物件](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)  
  
-   [通訊錄命令按鈕](../../../ado/guide/remote-data-service/address-book-command-buttons.md)  
  
-   [通訊錄導覽按鈕](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>請參閱  
 [通訊錄應用程式的系統需求](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)   
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [RDS 的基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)


