---
title: 搭配您的 Visual Basic 應用程式使用 VFP FoxPro ODBC 驅動程式 |Microsoft Docs
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
ms.openlocfilehash: 017e8e7897b2b792d7a864dc336537d76dcad8b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087982"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>搭配使用 VFP FoxPro ODBC Driver 與 Visual Basic 應用程式
您的 Microsoft® Visual Basic®應用程式可以藉由建立連接至 Visual FoxPro 資料來源的資料控制項，與 Visual FoxPro 資料進行通訊。  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>若要使用中的資料控制項連接到 Visual FoxPro 資料 Visual Basic  
  
1.  建立名為 "test" 的資料來源，以連接到包含在 Visual FoxPro 中的 TasTrade 範例資料庫。 預設的 Visual FoxPro 安裝會將 TasTrade 範例資料庫放在位置：  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  在 Visual Basic 中，建立新的表單，並在其中放置一個文字方塊和一個資料控制項。  
  
3.  變更資料控制項的 Connect 屬性，如下所示：  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  將 [當項] 屬性變更為下列內容：  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  將 [RecordSource] 屬性變更為下列內容：  
  
    ```  
    customer  
    ```  
  
6.  將文字方塊的 [DataSource] 屬性變更為 [資料] 控制項的預設名稱，如下所示：  
  
    ```  
    data1  
    ```  
  
7.  將文字方塊的 [DataField] 屬性變更為下列內容：  
  
    ```  
    customer_id  
    ```  
  
8.  執行表單，並使用資料控制項略過 Visual FoxPro TasTrade 範例資料庫中的客戶識別碼欄位。
