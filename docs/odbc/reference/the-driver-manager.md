---
title: 驅動程式管理員 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286792"
---
# <a name="the-driver-manager"></a>驅動程式管理員
*驅動程式管理員*是管理應用程式和驅動程式之間的通信的庫。 例如,在 Microsoft ® Windows ®平臺上,驅動程式管理器是一個動態連結庫 (DLL),由 Microsoft 編寫,並且可以由可再分發 MDAC 2.8 SP1 SDK 的使用者重新分發。  
  
 驅動程式管理員的存在主要是為了方便應用程式編寫器,並解決了所有應用程式共有的許多問題。 其中包括根據數據源名稱確定要載入的驅動程式、載入和卸載驅動程式以及驅動程式中的調用函數。  
  
 要瞭解後者為什麼存在問題,請考慮如果應用程式直接調用驅動程式中的函數會發生什麼情況。 除非應用程式直接連結到特定的驅動程式,否則它必須生成指向該驅動程式中函數的指標表,並通過指標調用這些函數。 一次對多個驅動程式使用相同的代碼將增加另一個複雜性級別。 應用程式首先必須設置函數指標以指向正確驅動程式中的正確函數,然後通過該指標調用該函數。  
  
 驅動程式管理員通過提供一個位置調用每個函數來解決此問題。 應用程式連結到驅動程式管理器,並在驅動程式管理器中調用ODBC函數,而不是驅動程式。 應用程式使用*連接句柄*標識目標驅動程式和數據源。 載入驅動程式時,驅動程式管理器將生成指向該驅動程式中函數的指標表。 它使用應用程式傳遞的連接句柄來尋找目標驅動程式中函數的位址,並按位址呼叫該函數。  
  
 在大多數情況下,驅動程式管理器只是將函數調用從應用程式傳遞到正確的驅動程式。 但是,它還實現了一些功能 **(SQLDataSources、SQLDrivers**和**SQLDrivers****SQLGet函數**),並執行基本錯誤檢查。 例如,驅動程式管理器檢查句柄不是空指標,函數是否按正確順序調用,並且某些函數參數是否有效。 有關驅動程式管理員檢查的錯誤的完整說明,請參閱每個函式的參考部分和[附錄 B:ODBC 狀態轉換表](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 駕駛員管理器的最後主要角色是裝載和卸載驅動程式。 應用程式僅載入和卸載驅動程式管理員。 當它想要使用特定的驅動程式時,它會在驅動程式管理器中調用連接函數 **(SQLConnect、SQLDriverConnect**或**SQLBrowse Connect),** 並指定特定資料源或驅動程式的名稱,例如「會計」或「SQL **SQLDriverConnect** Server」。。 使用此名稱,驅動程式管理器搜索驅動程式的檔名(如 Sqlsrvr.dll)的數據源資訊。 然後載入驅動程式(假設它尚未載入),將每個函數的位址儲存在驅動程式中,並在驅動程式中調用連接函數,然後初始化自身並連接到資料源。  
  
 使用驅動程式完成應用程式後,它將在驅動程式管理器中調用**SQLDISCONNECT。** 驅動程式管理器在驅動程式中呼叫此函數,該驅動程式與資料源斷開連接。 但是,驅動程式管理器將驅動程式保留在記憶體中,以防應用程式重新連接到它。 僅當應用程式釋放驅動程式使用的連接或為其他驅動程式使用連接時,它才會卸載驅動程式,並且沒有其他連接使用驅動程式。 有關驅動程式管理員在載入和卸載驅動程式中的角色的完整說明,請參閱[驅動程式管理器在連接過程中的角色](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。
