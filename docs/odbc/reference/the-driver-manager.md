---
title: 驅動程式管理員 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC]
- ODBC architecture [ODBC], driver manager
- driver manager [ODBC], about driver manager
- ODBC driver manager [ODBC]
ms.assetid: 559e4de1-16c9-4998-94f5-6431122040cd
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4d9a9c70743ee59ef347426fdac54e1e8667b33a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="the-driver-manager"></a>驅動程式管理員
*驅動程式管理員*是管理應用程式和驅動程式之間通訊的程式庫。 例如，Microsoft® Windows® 平台上，驅動程式管理員是動態連結程式庫 (DLL) 由 Microsoft 所撰寫，且使用者的可轉散發套件的 MDAC 2.8 SP1 sdk 可轉散發。  
  
 驅動程式管理員存在主要是為了方便起見應用程式寫入器，並解決一些通用於所有應用程式的問題。 其中包括決定要載入哪些驅動程式會根據資料來源名稱、 載入及卸載驅動程式，以及驅動程式中呼叫函式。  
  
 若要查看為什麼後者的問題，請考慮會發生什麼事應用程式函式的驅動程式中直接呼叫。 除非應用程式直接連結到特定的驅動程式，則可能會建立該驅動程式中的函式指標的資料表和呼叫這些函式指標。 一次使用一個以上的驅動程式的相同的程式碼會將另一個層級的複雜性。 應用程式會先設定以指向正確的驅動程式，在正確的函式的函式指標，然後呼叫透過該指標。  
  
 驅動程式管理員來解決這個問題，藉由呼叫每個函式的單一位置。 應用程式會連結到的驅動程式管理員和呼叫 ODBC 函數驅動程式管理員 中沒有驅動程式。 應用程式識別與目標驅動程式和資料來源*連接控制代碼*。 當它載入驅動程式時，驅動程式管理員會建立該驅動程式中的函式指標的資料表。 它會使用應用程式所傳遞的連接控制代碼目標驅動程式中尋找函式的位址，並呼叫此函式的位址。  
  
 大部分的情況下，驅動程式管理員才會傳遞從正確的驅動程式應用程式的函式呼叫。 不過，它也會實作某些函式 (**SQLDataSources**， **SQLDrivers**，和**SQLGetFunctions**) 並執行基本的錯誤檢查。 例如，驅動程式管理員會檢查控制代碼不是 null 指標，函式的呼叫正確的順序，且特定函式引數有效。 檢查驅動程式管理員錯誤的完整說明，請參閱每個函式的參考章節和[附錄 b: ODBC 狀態轉換表](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 最終的主要角色的驅動程式管理員會載入及卸載驅動程式。 應用程式載入及卸載驅動程式管理員。 當它想要使用的特定驅動程式時，它會呼叫連線函式 (**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**) 驅動程式管理員，並指定特定資料來源或驅動程式，例如 「 會計 」 或 「 SQL Server"的名稱 使用此名稱，則驅動程式管理員會搜尋驅動程式的檔案名稱，例如 Sqlsrvr.dll 的資料來源資訊。 接著會載入驅動程式 （假設未載入），將每個函式的位址儲存在驅動程式，並呼叫驅動程式，然後將其本身初始化並連接到資料來源中的連線函式。  
  
 完成應用程式時使用驅動程式，它會呼叫**SQLDisconnect**驅動程式管理員。 驅動程式管理員會呼叫此函式中的驅動程式中斷資料來源的連接。 不過，驅動程式管理員會保留驅動程式在記憶體中以防應用程式重新連線到它。 只有當應用程式釋放驅動程式所使用的連接或連接用於不同的驅動程式，而且沒有其他連接使用的驅動程式時，它會卸載驅動程式。 如需中載入及卸載驅動程式的驅動程式管理員角色的完整說明，請參閱[連線程序中的驅動程式管理員角色](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。
