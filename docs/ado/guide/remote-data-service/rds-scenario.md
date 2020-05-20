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
author: rothja
ms.author: jroth
ms.openlocfilehash: d73bb03ceb08e61257c0e4fc6d3f6a627ddb746d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763579"
---
# <a name="rds-scenario"></a>RDS 案例
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 通訊錄應用程式是一種案例，示範如何使用遠端資料服務（RDS）來建立簡單的資料感知 Web 應用程式，也就是線上的公司通訊錄。 此案例適用于想要瞭解如何搭配 RDS 使用資料感知 ActiveX 控制項的 Microsoft Visual Basic Scripting Edition （VBScript）和 COM 程式設計人員，以及想要建立以資料為中心之 Web 應用程式的更有經驗的軟體發展人員。  
  
 此案例假設您知道如何使用基本的 HTML 版面配置標記、使用 DHTML 資料系結技術，並以 ActiveX 控制項進行程式設計。  
  
 如果您已安裝 SDK，則可以在 SDK 目錄中找到通訊錄範例應用程式的完整原始程式碼，網址為 samples\dataaccess\rds\AddressBook\AddressBook.asp.。 若要查看通訊錄案例，請在 Internet Explorer 4.0 或更新版本中輸入**HTTPs://*web*伺服器/RDS/AddressBook/AddressBook.asp** ，其中*web*伺服器是提供給執行 Internet Information Services （IIS）和 Asp 的 Windows NT 4.0 或 windows 2000 Web 服務器電腦的名稱。  
  
## <a name="introduction-to-address-book"></a>通訊錄簡介  
 通訊錄範例應用程式會提供簡單的線上通訊錄，供您用來透過內部網路發佈可搜尋的目錄。 通訊錄的設計可讓使用者在一或多個欄位中輸入搜尋字串，以要求員工的相關資訊。 為了說明遠端資料服務的基本功能，範例應用程式會刻意以較小的物件和搜尋欄位數目來保存。  
  
 應用程式介面包含下列元件：  
  
-   非 visual **RDS。DataControl**資料系結物件，由用戶端用來連接到資料庫。  
  
-   作為 employee 屬性搜尋準則之輸入欄位的 HTML 文字方塊。  
  
-   用來建立查詢、清除搜尋欄位、以員工資訊更新資料庫、取消暫止的變更，以及流覽方格中所顯示資料列的 HTML 命令按鈕。  
  
-   DHTML 資料系結，可顯示針對後端資料庫（透過 RDS）從查詢傳回的資料 **。DataControl**資料系結物件）在資料表中。  
  
-   一種 VBScript 常式，會連接先前提及的每個專案，並允許它們進行互動。 VBScript 程式碼也會用來初始化**RDS。DataControl**物件，並從 RDS 的名稱在 HTML 資料表中動態建立資料行標題 **。DataControl**記錄集欄位。  
  
 遵循逐步執行的連結來設定及執行案例，並深入瞭解此案例的運作方式。  
  
 此案例包含下列主題。  
  
-   [通訊錄應用程式的系統需求](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)  
  
-   [執行通訊錄 SQL 指令碼](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)  
  
-   [執行通訊錄範例應用程式](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)  
  
-   [通訊錄資料繫結物件](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)  
  
-   [通訊錄命令按鈕](../../../ado/guide/remote-data-service/address-book-command-buttons.md)  
  
-   [通訊錄導覽按鈕](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>另請參閱  
 [通訊錄應用程式的系統需求](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)   
 [Microsoft ActiveX Data Objects （ADO）](../../../ado/microsoft-activex-data-objects-ado.md)   
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)


