---
description: 資料長度、緩衝區長度和截斷
title: 資料長度、緩衝區長度和截斷 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- data length [ODBC]
- truncating data [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 2825c6e7-b9ff-42fe-84fc-7fb39728ac5d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c9a9651f39c1ff4d2c6dc9b691453fb5354c9e1a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465830"
---
# <a name="data-length-buffer-length-and-truncation"></a>資料長度、緩衝區長度和截斷
*資料長度*是資料的位元組長度，因為它會儲存在應用程式的資料緩衝區中，而不是儲存在資料來源中。 這項區別很重要，因為資料通常儲存在資料緩衝區中的不同類型中，而不是資料來源中。 因此，對於要傳送到資料來源的資料，這是轉換成資料來源類型之前的資料位元組長度。 針對從資料來源抓取的資料，這是轉換成資料緩衝區類型之後，以及在任何截斷完成之前的資料位元組長度。  
  
 若為固定長度的資料（例如整數或日期結構），資料的位元組長度一律為資料類型的大小。 一般而言，應用程式會配置資料類型大小的資料緩衝區。 如果應用程式佈建較小的緩衝區，則會產生未定義的結果，因為驅動程式會假設資料緩衝區是資料類型的大小，且不會截斷資料以符合較小的緩衝區。 如果應用程式佈建較大的緩衝區，就不會使用額外的空間。  
  
 對於可變長度的資料（例如字元或二進位資料），請務必辨識資料的位元組長度是分開的，而且通常與緩衝區的位元組長度不同。 這兩個長度的關聯會在 [ [緩衝區](../../../odbc/reference/develop-app/buffers.md) ] 區段中描述。 如果資料的位元組長度大於緩衝區的位元組長度，驅動程式會將提取的資料截斷為緩衝區的位元組長度，並傳回 SQLSTATE 01004 (資料截斷) 的 SQL_SUCCESS_WITH_INFO。 不過，傳回的位元組長度是 untruncated 資料的長度。  
  
 例如，假設應用程式會為二進位資料緩衝區配置50個位元組。 如果驅動程式有10個位元組的二進位資料要傳回，它會在緩衝區中傳回10個位元組。 資料的位元組長度為10，而緩衝區的位元組長度為50。 如果驅動程式具有60個位元組的二進位資料要傳回，就會將資料截斷為50個位元組，並傳回緩衝區中的這些位元組，並傳回 SQL_SUCCESS_WITH_INFO。 資料的位元組長度是 60 (截斷) 之前的長度，而緩衝區的位元組長度仍然是50。  
  
 針對截斷的每個資料行建立診斷記錄。 因為驅動程式需要一些時間來建立這些記錄，並讓應用程式處理這些記錄，所以截斷可能會降低效能。 通常，應用程式可以配置夠大的緩衝區來避免此問題，不過在使用長資料時可能無法這麼做。 發生資料截斷時，應用程式有時會配置較大的緩衝區並重新擷取資料;這在所有情況下都不是如此。 如果在透過呼叫 **SQLGetData**取得資料時發生截斷，則應用程式不需要針對已經傳回的資料呼叫 **SQLGetData** ;如需詳細資訊，請參閱 [取得較長的資料](../../../odbc/reference/develop-app/getting-long-data.md)。
