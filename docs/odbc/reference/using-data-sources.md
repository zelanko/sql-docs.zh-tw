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
manager: craigg
ms.openlocfilehash: c898cb5cd8c9998d9126ec468a2b43587e2e279a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47728106"
---
# <a name="using-data-sources"></a>使用資料來源
建立資料來源通常是由使用者或技術人員的程式稱為*ODBC 管理員*。 ODBC 管理員會提示使用者輸入驅動程式來使用，然後再撥打該驅動程式。 驅動程式會顯示一個對話方塊，要求它需要連接到資料來源的資訊。 使用者輸入的資訊之後，驅動程式會將它儲存在系統上。  
  
 更新版本中，應用程式會呼叫驅動程式管理員，並將它傳遞的機器資料來源名稱或包含檔案資料來源的檔案路徑。 當傳遞的機器資料來源名稱，驅動程式管理員會搜尋系統以尋找資料來源所使用的驅動程式。 接著會載入驅動程式，並傳遞給它的資料來源的名稱。 驅動程式會使用資料來源名稱來尋找它需要連接到資料來源的資訊。 最後，它會連接到資料來源，通常提示使用者輸入使用者識別碼和密碼，這通常不會儲存。  
  
 當傳遞的資料來源時，驅動程式管理員就會開啟檔案，並載入指定的驅動程式。 如果檔案也包含連接字串，它會將此驅動程式。 連接字串中使用的資訊，此驅動程式會連接到資料來源。 如果不傳遞任何連接字串，則驅動程式通常會提示使用者輸入所需的資訊。
