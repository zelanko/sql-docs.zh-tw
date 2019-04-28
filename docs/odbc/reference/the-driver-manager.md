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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0c1ae3f098aea3886d5cb84a0bfcb7553a8181fa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62719733"
---
# <a name="the-driver-manager"></a>驅動程式管理員
*驅動程式管理員*是管理應用程式和驅動程式之間的通訊程式庫。 例如，在 Microsoft® Windows® 平台，驅動程式管理員是動態連結程式庫 (DLL) 由 Microsoft 所撰寫，並可轉散發的可轉散發套件的 MDAC 2.8 SP1 SDK 使用者。  
  
 驅動程式管理員存在主要是為了方便應用程式撰寫者，並解決一些通用於所有的應用程式的問題。 其中包括決定要載入哪些驅動程式會根據資料來源名稱、 載入及卸載驅動程式，以及驅動程式中呼叫函式。  
  
 若要查看後者為何有問題，請考慮會發生什麼事如果應用程式函式中的驅動程式直接呼叫。 除非應用程式的直接連結到特定的驅動程式，您必須建置該驅動程式中函式指標的資料表，並由指標呼叫這些函式。 一次使用一個以上的驅動程式的相同的程式碼會新增另一層複雜度。 應用程式第一次設定函式指標以指向正確的函式，在正確的驅動程式，並接著呼叫的函式，透過該指標。  
  
 驅動程式管理員會提供單一位置來呼叫每個函式，以解決這個問題。 應用程式已連結的驅動程式管理員和呼叫 ODBC 函數中的驅動程式管理員 中，不是驅動程式。 應用程式識別與目標驅動程式和資料來源*連接控制代碼*。 當它載入驅動程式時，驅動程式管理員會建立該驅動程式中函式指標的資料表。 它會使用應用程式所傳遞的連接控制代碼目標驅動程式中尋找函式的位址，並呼叫該函式的位址。  
  
 大部分的情況下，驅動程式管理員只會將傳遞從正確的驅動程式應用程式的函式呼叫。 不過，它也會實作某些函式 (**SQLDataSources**， **SQLDrivers**，並**SQLGetFunctions**)，並執行基本的錯誤檢查。 例如，驅動程式管理員會檢查控制代碼不是 null 指標，函式會呼叫正確的順序，和特定的函式引數都有效。 檢查驅動程式管理員錯誤的完整說明，請參閱 [參考] 區段，每個函式和[附錄 b:狀態轉換資料表](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 最終的主要角色的驅動程式管理員會載入及卸載驅動程式。 應用程式載入及卸載驅動程式管理員。 當它想要使用的特定驅動程式時，它會呼叫連接函式 (**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**) 在驅動程式管理員，並指定特定資料來源或驅動程式，例如 「 會計 」 或 「 SQL Server。 」 的名稱 使用此名稱，則驅動程式管理員會搜尋驅動程式的檔案名稱，例如 Sqlsrvr.dll 的資料來源資訊。 然後會載入驅動程式 （假設未載入），將每個函式的位址儲存在驅動程式，並呼叫驅動程式，然後自行初始化，並連接到資料來源中的連線函式。  
  
 完成應用程式使用驅動程式，它會呼叫**SQLDisconnect**驅動程式管理員。 驅動程式管理員會呼叫此函式中從資料來源中斷連線的驅動程式。 不過，驅動程式管理員會保留驅動程式在記憶體中萬一應用程式重新連接到它。 只有在應用程式釋出驅動程式所使用的連接，或連接用於不同的驅動程式，並沒有其他連接使用的驅動程式時，它會卸載該驅動程式。 中載入及卸載驅動程式的驅動程式管理員角色的完整說明，請參閱[在連線程序中的驅動程式管理員角色](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。
