---
description: 搭配使用 VFP FoxPro ODBC Driver 與 Visual Basic 應用程式
title: 使用 VFP FoxPro ODBC 驅動程式搭配您的 Visual Basic 應用程式 |Microsoft Docs
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
ms.openlocfilehash: 07ec83ccab43890bccbf5e12582628fdb98d29c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500051"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>搭配使用 VFP FoxPro ODBC Driver 與 Visual Basic 應用程式
您的 Microsoft® Visual Basic®應用程式可以藉由建立連接到 Visual FoxPro 資料來源的資料控制來與 Visual FoxPro 資料進行通訊。  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>使用 Visual Basic 中的資料控制連接到 Visual FoxPro 資料  
  
1.  建立名為 "test" 的資料來源，以連接到包含在 Visual FoxPro 中的 TasTrade 範例資料庫。 預設的 Visual FoxPro 安裝會將 TasTrade 範例資料庫放在位置：  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  在 Visual Basic 中，建立新的表單，並將文字方塊和資料控制項放在其上。  
  
3.  變更資料控制的 Connect 屬性，如下所示：  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  將 [變更] 屬性變更為下列內容：  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  將 [記錄] 屬性變更為下列內容：  
  
    ```  
    customer  
    ```  
  
6.  將文字方塊的 [DataSource] 屬性變更為 [資料] 控制項的預設名稱，如下所示：  
  
    ```  
    data1  
    ```  
  
7.  將文字方塊的 DataField 屬性變更為下列內容：  
  
    ```  
    customer_id  
    ```  
  
8.  執行表單，然後使用資料控制略過 Visual FoxPro TasTrade 範例資料庫中的客戶識別碼欄位。
