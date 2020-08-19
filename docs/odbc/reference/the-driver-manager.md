---
description: 驅動程式管理員
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
ms.openlocfilehash: 70508eba3f5fce81c6f6185f0ec6befbe0d33b26
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428870"
---
# <a name="the-driver-manager"></a>驅動程式管理員
*驅動程式管理員*是一個程式庫，可管理應用程式與驅動程式之間的通訊。 例如，在 Microsoft® Windows®平臺上，驅動程式管理員是 Microsoft 撰寫的動態連結程式庫 (DLL) ，可轉散發 MDAC 2.8 SP1 SDK 的使用者轉散發。  
  
 驅動程式管理員主要是做為應用程式寫入器的便利性，可解決所有應用程式常見的一些問題。 這些包括根據資料來源名稱、載入和卸載驅動程式，以及在驅動程式中呼叫函式來決定要載入的驅動程式。  
  
 若要查看第二個問題的原因，請考慮應用程式直接在驅動程式中呼叫函式時，會發生什麼事。 除非應用程式直接連結到特定的驅動程式，否則就必須建立指向該驅動程式之函式的指標表格，並依指標呼叫這些函數。 一次針對一個以上的驅動程式使用相同的程式碼會增加另一層的複雜度。 應用程式必須先設定函式指標，以指向正確驅動程式中正確的函式，然後透過該指標呼叫函式。  
  
 驅動程式管理員會提供單一位置來呼叫每個函式，藉此解決這個問題。 應用程式會連結到驅動程式管理員，並在驅動程式管理員中呼叫 ODBC 函數，而不是驅動程式。 應用程式會使用 *連接控制碼*來識別目標驅動程式和資料來源。 當它載入驅動程式時，驅動程式管理員會建立該驅動程式之函式的指標表格。 它會使用應用程式所傳遞的連接控制碼，在目標驅動程式中尋找函式的位址，並依位址呼叫該函式。  
  
 在大部分的情況下，驅動程式管理員只會將函式呼叫從應用程式傳遞到正確的驅動程式。 不過，它也會實 (**SQLDataSources**、 **SQLDrivers**和 **SQLGetFunctions**) 的一些函數，並執行基本錯誤檢查。 例如，驅動程式管理員會檢查控制碼不是 null 指標，該函式會以正確的順序呼叫，且特定的函式引數有效。 如需驅動程式管理員所檢查之錯誤的完整說明，請參閱每個函式的參考章節和 [附錄 B： ODBC 狀態轉換資料表](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 驅動程式管理員的最後主要角色是載入和卸載驅動程式。 應用程式只會載入並卸載驅動程式管理員。 當它想要使用特定的驅動程式時，它會在驅動程式管理員中呼叫 (**SQLConnect**、 **SQLDriverConnect**或 **SQLBrowseConnect**) 的連接函數，並指定特定資料來源或驅動程式的名稱，例如 "Accounting" 或 "SQL Server"。 驅動程式管理員會使用此名稱來搜尋資料來源資訊，以取得驅動程式的檔案名，例如 Sqlsrvr.dll。 然後，它會載入驅動程式 (假設尚未載入) 、將每個函式的位址儲存在驅動程式中，並呼叫驅動程式中的連接函式，然後初始化本身並連接到資料來源。  
  
 當應用程式使用驅動程式完成時，它會在驅動程式管理員中呼叫 **SQLDisconnect** 。 驅動程式管理員會在驅動程式中呼叫此函式，此函式會中斷與資料來源的連線。 不過，驅動程式管理員會在應用程式重新連接到記憶體時，將驅動程式保留在記憶體中。 只有當應用程式釋放驅動程式所使用的連線，或針對不同的驅動程式使用該連接，而且沒有其他連線使用驅動程式時，它才會卸載驅動程式。 如需驅動程式管理員在載入和卸載驅動程式中的角色的完整說明，請參閱 [連接程式中的驅動程式管理員角色](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。
