---
title: SQLDriverConnect （Visual FoxPro ODBC Driver） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307089"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 支援：完整  
  
 ODBC API 一致性：層級1  
  
 連接到現有的資料來源，它可以是[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)或[可用資料表](../../odbc/microsoft/visual-foxpro-terminology.md)的目錄。 ODBC 屬性關鍵字 UID 和 PWD 會被忽略。 下表列出其他支援的屬性關鍵字。  
  
|ODBC attribute 關鍵字|屬性值|  
|----------------------------|---------------------|  
|DSN||  
|UID|由 Visual FoxPro ODBC 驅動程式忽略，但不會產生錯誤。|  
|PWD|由 Visual FoxPro ODBC 驅動程式忽略，但不會產生錯誤。|  
|驅動程式|Visual FoxPro ODBC 驅動程式的名稱和位置;由驅動程式管理員執行。|  
  
|Visual FoxPro ODBC Driver attribute 關鍵字|屬性值|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|「是」或「否」|  
|自動分頁|「電腦」或其他定序序列。 如需支援的定序序列清單，請參閱[SET COLLATE](../../odbc/microsoft/set-collate-command.md)。|  
|描述||  
|獨佔|「是」或「否」|  
|SourceDB|包含零個或多個[可用資料表](../../odbc/microsoft/visual-foxpro-terminology.md)之目錄的完整路徑，或[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)的絕對路徑和檔案名。|  
|SourceType|"DBC" 或 "DBF"|  
|版本||  
  
 如果未指定資料來源名稱，驅動程式管理員會提示使用者提供資訊（視*fDriverCompletion*引數的設定而定），然後繼續進行。 如果需要詳細資訊，Visual FoxPro ODBC 驅動程式會顯示 [提示] 對話方塊。  
  
 如需詳細資訊，請參閱 ODBC 程式設計*人員參考*中的[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) 。
