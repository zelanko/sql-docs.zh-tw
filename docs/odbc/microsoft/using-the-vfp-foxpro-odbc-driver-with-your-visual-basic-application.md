---
title: 將 VFP FoxPro ODBC 驅動程式與您的視覺基本應用程式一起使用 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 871c392166fa2f5726e6f9e8651bf758dc144a00
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292698"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>搭配使用 VFP FoxPro ODBC Driver 與 Visual Basic 應用程式
您的 Microsoft®可視化基礎®應用程式可以通過創建連接到 Visual FoxPro 資料源的數據控制件與 Visual FoxPro 資料進行通訊。  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>使用視覺化基礎中的資料控制到 Visual FoxPro 資料  
  
1.  創建名為"測試"的數據源,該資料源連接到 Visual FoxPro 中包含的 TasTrade 範例資料庫。 預設的 Visual FoxPro 安裝將 TasTrade 範例資料庫放在該位置:  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  在"視覺基本"中,創建新窗體,並在其中放置一個文本框和數據控件。  
  
3.  更改「數據」控制項的 Connect 屬性,如下所示:  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  將紀錄集類型屬性變更為以下內容:  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  將 RecordSource 屬性變更為以下內容:  
  
    ```  
    customer  
    ```  
  
6.  將文字框的 DataSource 屬性變更為「資料」控制項預設名稱,改變為以下內容:  
  
    ```  
    data1  
    ```  
  
7.  將文字框的 DataField 屬性變更為以下內容:  
  
    ```  
    customer_id  
    ```  
  
8.  執行表單,並使用資料控制件跳過 Visual FoxPro TasTrade 範例資料庫中的客戶 ID 欄位。
