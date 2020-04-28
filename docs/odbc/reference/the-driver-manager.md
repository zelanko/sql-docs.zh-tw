---
title: 驅動程式管理員 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC]
- ODBC architecture [ODBC], driver manager
- driver manager [ODBC], about driver manager
- ODBC driver manager [ODBC]
ms.assetid: 559e4de1-16c9-4998-94f5-6431122040cd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 686a2b9673fb392f969a42f4cc86dd95a95668a6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286792"
---
# <a name="the-driver-manager"></a>驅動程式管理員
*驅動程式管理員*是一種程式庫，可管理應用程式與驅動程式之間的通訊。 例如，在 Microsoft® Windows®平臺上，驅動程式管理員是由 Microsoft 撰寫的動態連結程式庫（DLL），可轉散發 MDAC 2.8 SP1 SDK 的使用者重新發佈。  
  
 驅動程式管理員主要是為了方便應用程式寫入器使用，並可解決所有應用程式通用的許多問題。 其中包括根據資料來源名稱來決定要載入的驅動程式、載入和卸載驅動程式，以及呼叫驅動程式中的函式。  
  
 若要查看第二個問題的原因，請考慮當應用程式直接在驅動程式中呼叫函式時，會發生什麼情況。 除非應用程式已直接連結到特定的驅動程式，否則必須建立該驅動程式中函式的指標資料表，並依指標呼叫這些函式。 一次對多個驅動程式使用相同的程式碼，會增加另一層的複雜度。 應用程式必須先將函式指標設定為指向正確驅動程式中的正確函式，然後透過該指標呼叫函式。  
  
 驅動程式管理員藉由提供單一位置來呼叫每個函式，來解決這個問題。 應用程式會連結到驅動程式管理員，並呼叫驅動程式管理員中的 ODBC 函式，而不是驅動程式。 應用程式會使用*連接控制碼*來識別目標驅動程式和資料來源。 當它載入驅動程式時，驅動程式管理員會建立該驅動程式中函式的指標表格。 它會使用應用程式所傳遞的連接控制碼，來尋找目標驅動程式中的函式位址，並依位址呼叫該函式。  
  
 在大部分情況下，驅動程式管理員只會將函式呼叫從應用程式傳遞至正確的驅動程式。 不過，它也會實行一些函式（**SQLDataSources**、 **SQLDrivers**和**SQLGetFunctions**），並執行基本錯誤檢查。 例如，驅動程式管理員會檢查控制碼不是 null 指標，函式會以正確的順序呼叫，而且特定的函式引數是有效的。 如需驅動程式管理員所檢查之錯誤的完整描述，請參閱每個函式的參考章節和[附錄 B： ODBC 狀態轉換資料表](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 驅動程式管理員的最後一個主要角色是載入和卸載驅動程式。 應用程式只會載入及卸載驅動程式管理員。 當它想要使用特定的驅動程式時，它會在驅動程式管理員中呼叫連接功能（**SQLConnect**、 **SQLDriverConnect**或**SQLBrowseConnect**），並指定特定資料來源或驅動程式的名稱，例如 "Accounting" 或 "SQL Server"。 使用此名稱時，驅動程式管理員會搜尋資料來源資訊中是否有驅動程式的檔案名，例如 Sqlsrvr。 然後，它會載入驅動程式（假設尚未載入）、將每個函式的位址儲存在驅動程式中，然後在驅動程式中呼叫連接函式，然後將其初始化並連接至資料來源。  
  
 當應用程式使用驅動程式完成時，它會呼叫驅動程式管理員中的**SQLDisconnect** 。 驅動程式管理員會在驅動程式中呼叫此函式，此功能會中斷與資料來源的連線。 不過，驅動程式管理員會在應用程式重新連接時，將驅動程式保留在記憶體中。 只有當應用程式釋出驅動程式所使用的連線，或針對不同的驅動程式使用連線，而且沒有其他連接使用驅動程式時，才會卸載驅動程式。 如需驅動程式管理員在載入和卸載驅動程式之角色的完整描述，請參閱[連接程式中的驅動程式管理員角色](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。
