---
title: SQLDriverConnect(可視化福克斯Pro ODBC驅動程式) |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e270f8c9be42dc109adeaa49acb84f29f2b9511
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307089"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援: 完整  
  
 ODBC API 符合性:1 級  
  
 連接到現有數據源,資料來源可以是[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)或[可用表](../../odbc/microsoft/visual-foxpro-terminology.md)的目錄。 ODBC 屬性關鍵字 UID 和 PWD 將被忽略。 下表列出了其他受支援的屬性關鍵字。  
  
|ODBC 屬性關鍵字|屬性值|  
|----------------------------|---------------------|  
|DSN||  
|UID|被 Visual FoxPro ODBC 驅動程式忽略,但不會生成錯誤。|  
|PWD|被 Visual FoxPro ODBC 驅動程式忽略,但不會生成錯誤。|  
|驅動程式|視覺福克斯Pro ODBC驅動程式的名稱和位置;由驅動程式管理員實施。|  
  
|視覺化福斯Pro ODBC驅動程式屬性關鍵字|屬性值|  
|-------------------------------------------------|---------------------|  
|背景擷取|"是"或"否"|  
|自動分頁|"機器"或其他整理序列。 有關支援的整理序列的清單,請參閱[SET COLLATE](../../odbc/microsoft/set-collate-command.md)。|  
|描述||  
|獨佔|"是"或"否"|  
|SourceDB|包含零個或多個[可用表](../../odbc/microsoft/visual-foxpro-terminology.md)的目錄的完全限定路徑,或[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)的絕對路徑和檔名。|  
|SourceType|"DBC"或"DBF"|  
|版本||  
  
 如果未指定資料源名稱,驅動程式管理員會提示使用者提供資訊(取決於*fDriver 完成*參數的設置),然後繼續。 如果需要更多資訊,可視化 FoxPro ODBC 驅動程式將顯示提示對話方塊。  
  
 有關詳細資訊,請參閱*ODBC 程式師參考*中的[SQLDriverConnect。](../../odbc/reference/syntax/sqldriverconnect-function.md)
