---
title: 使用資料來源 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], about data sources
ms.assetid: d5550619-22b2-4b16-bd08-fbabb6554c40
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 52015cb202f46c50c16dcab408bed7761f0925db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67951808"
---
# <a name="using-data-sources"></a>使用資料來源
資料來源通常是由終端使用者或具有稱為「 *ODBC 系統管理員*」之程式的技術人員所建立。 ODBC 系統管理員會提示使用者提供要使用的驅動程式，然後再呼叫該驅動程式。 驅動程式會顯示一個對話方塊，要求其連接到資料來源所需的資訊。 在使用者輸入資訊之後，驅動程式會將它儲存在系統上。  
  
 之後，應用程式會呼叫驅動程式管理員，並將電腦資料來源的名稱或包含檔案資料來源之檔案的路徑傳遞給它。 當傳遞電腦資料來源名稱時，驅動程式管理員會搜尋系統，以尋找資料來源所使用的驅動程式。 然後，它會載入驅動程式，並將資料來源名稱傳遞給它。 驅動程式會使用資料來源名稱來尋找連接到資料來源所需的資訊。 最後，它會連接到資料來源，通常會提示使用者輸入使用者識別碼和密碼，這通常不會儲存。  
  
 當傳遞檔案資料來源時，驅動程式管理員會開啟檔案，並載入指定的驅動程式。 如果檔案也包含連接字串，則會將它傳遞給驅動程式。 使用連接字串中的資訊，驅動程式會連接到資料來源。 如果未傳遞任何連接字串，驅動程式通常會提示使用者提供必要的資訊。
