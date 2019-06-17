---
title: SQLDriverConnect (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 10492c8f-3a18-4971-9db8-879e878083b9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc0bcf6a191f67b87b422b17778f56feda1f5227
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63238084"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援：完整  
  
 ODBC API 相容性：層級 1  
  
 連接到現有的資料來源，這可以是[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)或是的目錄[免費資料表](../../odbc/microsoft/visual-foxpro-terminology.md)。 UID 和 PWD ODBC 屬性關鍵字會被忽略。 下表列出的其他支援的屬性關鍵字。  
  
|ODBC 屬性關鍵字|屬性值|  
|----------------------------|---------------------|  
|DSN||  
|UID|Visual FoxPro ODBC Driver 被忽略，但不會產生錯誤。|  
|PWD|Visual FoxPro ODBC Driver 被忽略，但不會產生錯誤。|  
|驅動程式|名稱和位置的 Visual FoxPro ODBC Driver;實作由驅動程式管理員。|  
  
|Visual FoxPro ODBC Driver 屬性關鍵字|屬性值|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"Yes"或者"No"|  
|自動分頁|「 電腦 」 或其他定序的順序。 如需支援的定序順序的清單，請參閱 <<c0> [ 設定定序](../../odbc/microsoft/set-collate-command.md)。|  
|描述||  
|排除|"Yes"或者"No"|  
|SourceDB|完整的路徑的目錄，包含零個或多個[免費資料表](../../odbc/microsoft/visual-foxpro-terminology.md)，或為絕對路徑和檔案名稱[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)。|  
|SourceType|「 雙位元組字元"或者"DBF"|  
|版本||  
  
 如果未指定資料來源名稱，驅動程式管理員 會提示使用者輸入資訊 (視設定而定*fDriverCompletion*引數)，然後再繼續。 如果需要詳細資訊，Visual FoxPro ODBC Driver 就會顯示提示的對話方塊。  
  
 如需詳細資訊，請參閱 < [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)中*ODBC 程式設計人員參考*。
