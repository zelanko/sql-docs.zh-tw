---
description: 執行緒支援 (Visual FoxPro ODBC Driver)
title: " (Visual FoxPro ODBC Driver) 的執行緒支援 |Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- thread support [ODBC]
- Visual FoxPro ODBC driver [ODBC], thread support
- FoxPro ODBC driver [ODBC], thread support
- multithreaded applications [ODBC]
ms.assetid: 0c6abbbc-012b-41aa-bded-5e7e362d015b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 013ccd1f5d202794ba6b7a44c10339dd14c08d17
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449070"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>執行緒支援 (Visual FoxPro ODBC Driver)
Visual FoxPro ODBC 驅動程式是安全線程。 存取環境會處理 (*抽*) 、連接處理 (*hdbc*) 和語句控制碼 (*hstmt*) 會包裝在適當的信號中，以防止其他進程存取並可能變更驅動程式的內部資料結構。  
  
 在多執行緒應用程式中，您可以在個別的執行緒上呼叫[SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md) ，以取消在*hstmt*上同步執行的函數。  
  
 當您使用漸進式提取時，驅動程式會使用個別的執行緒來提取資料。 若要使用資料來源的漸進式提取，請在 [ [ODBC Visual FoxPro 安裝程式] 對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)中選取 [**在背景中提取資料**] 核取方塊，或在您的連接字串中使用 BackgroundFetch 屬性關鍵字。 當您從多執行緒應用程式呼叫驅動程式時，請避免使用背景提取。 如需連接字串屬性關鍵字的詳細資訊，請參閱 [使用連接字串](../../odbc/microsoft/using-connection-strings.md)。  
  
 如需有關執行緒和**SQLCancel**的詳細資訊，請參閱《 ODBC 程式設計*人員參考*》中的[SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md) 。
