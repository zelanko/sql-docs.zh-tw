---
title: Visual Basic 應用程式搭配使用 VFP FoxPro ODBC Driver |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], visual basic applications
- Visual Basic applications [ODBC]
- FoxPro ODBC driver [ODBC], visual basic applications
- Visual FoxPro data [ODBC], visual basic applications
ms.assetid: 5223ca23-5df6-4ebc-aa3b-70682ff27a8c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b77fdee70ff73772710c9758eeb2bf2594f365d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280946"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>搭配使用 VFP FoxPro ODBC Driver 與 Visual Basic 應用程式
您的 Microsoft® Visual Basic® 應用程式可以使用 Visual FoxPro 資料進行通訊，藉由建立連接到 Visual FoxPro 資料來源的資料控制項。  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>若要連接到 Visual Basic 中使用資料控制項的 Visual FoxPro 資料  
  
1.  建立連接至 TasTrade 範例資料庫包含在 Visual FoxPro 資料來源名為"test"。 預設 Visual FoxPro 安裝位置中放置 TasTrade 範例資料庫：  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  在 Visual Basic 中建立新的表單並將文字方塊和資料控制項在其上。  
  
3.  將資料控制項的 [Connect] 屬性變更，如下所示：  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  變更記錄集類型屬性如下：  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  變更記錄資料來源屬性如下：  
  
    ```  
    customer  
    ```  
  
6.  將資料來源屬性的文字方塊中，以下列的資料控制項的預設名稱變更：  
  
    ```  
    data1  
    ```  
  
7.  將文字方塊的 DataField 屬性變更為下列：  
  
    ```  
    customer_id  
    ```  
  
8.  執行表單，並使用 Visual FoxPro TasTrade 範例資料庫中略過透過客戶識別碼欄位的資料控制項。
