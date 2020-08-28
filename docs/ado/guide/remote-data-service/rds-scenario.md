---
description: RDS 案例
title: RDS 案例 |Microsoft Docs
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
ms.assetid: a7dcad87-aaf0-4b02-9660-472f8469761c
author: rothja
ms.author: jroth
ms.openlocfilehash: e4492a80690c99d1e5b7003763faf77effdeebec
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977879"
---
# <a name="rds-scenario"></a>RDS 案例
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 通訊錄的應用程式是一種案例，示範如何使用遠端資料服務 (RDS) 建立簡單、資料感知的 Web 應用程式，也就是線上的公司通訊錄。 這種情況適用于 Microsoft Visual Basic Scripting Edition (VBScript) 以及想要瞭解如何使用 RDS 的資料感知 ActiveX 控制項，以及更有經驗的軟體發展人員想要建立以資料為中心的 Web 應用程式時，這種情況很有用。  
  
 此案例假設您知道如何使用基本的 HTML 版面配置標記、使用 DHTML 資料系結技術，以及使用 ActiveX 控制項進行程式設計。  
  
 如果您已安裝 SDK，您可以在 SDK 目錄中找到通訊錄範例應用程式的完整原始程式碼，網址是 samples\dataaccess\rds\AddressBook\AddressBook.asp。 若要查看通訊錄案例，請在 Internet Explorer 4.0 或更新版本中輸入 **HTTPs://*web 伺服器*/RDS/AddressBook/AddressBook.asp** ，其中 *web* 伺服器是提供給 Windows NT 4.0 或 Windows 2000 Web 服務器電腦的名稱，該電腦是執行 Internet Information Services (IIS) 和 asp。  
  
## <a name="introduction-to-address-book"></a>通訊錄簡介  
 通訊錄範例應用程式提供簡單的線上通訊錄，您可以用來透過內部網路發佈可搜尋的目錄。 通訊錄的設計目的是讓使用者可以在一或多個欄位中輸入搜尋字串，以要求員工的相關資訊。 為了顯示遠端資料服務的基本功能，範例應用程式會刻意保持很小，並具有最少的物件和搜尋欄位數目。  
  
 應用程式介面是由下列部分所組成：  
  
-   非視覺效果 **RDS。DataControl** 用戶端用來連接到資料庫的資料系結物件。  
  
-   HTML 文字方塊，作為員工屬性搜尋準則的輸入欄位。  
  
-   用來建立查詢、清除搜尋欄位、以員工資訊更新資料庫、取消暫止的變更，以及流覽方格中所顯示資料列的 HTML 命令按鈕。  
  
-   DHTML 資料系結，可顯示針對後端資料庫從查詢傳回的資料， (透過 **RDS。DataControl** 資料表中的資料系結物件) 。  
  
-   VBScript 常式，可連接先前提及的每個專案並允許它們互動。 VBScript 程式碼也用來初始化 **RDS。DataControl** 物件，並在 HTML 資料表中從 RDS 的名稱動態建立資料行標題 **。DataControl** 記錄集欄位。  
  
 遵循逐步解說中的連結來設定和執行案例，並深入瞭解此案例的運作方式。  
  
 此案例包含下列主題。  
  
-   [通訊錄應用程式的系統需求](./system-requirements-for-the-address-book-application.md)  
  
-   [執行通訊錄 SQL 指令碼](./running-the-address-book-sql-script.md)  
  
-   [執行通訊錄應用程式範例](./running-the-address-book-sample-application.md)  
  
-   [通訊錄資料繫結物件](./address-book-data-binding-object.md)  
  
-   [通訊錄命令按鈕](./address-book-command-buttons.md)  
  
-   [通訊錄導覽按鈕](./address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>另請參閱  
 [通訊錄應用程式的系統需求](./system-requirements-for-the-address-book-application.md)   
 [Microsoft ActiveX Data Objects (ADO) ](../../microsoft-activex-data-objects-ado.md)   
 [RDS 基本概念](./rds-fundamentals.md)   
 [RDS 教學課程](./rds-tutorial.md)