---
title: ODBC 驅動程式架構 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], architecture
ms.assetid: 21a62c7c-192e-4718-a16e-aa12b0de4419
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9566599b68ac931604ab68c06da2f6cd624673fe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32917323"
---
# <a name="odbc-driver-architecture"></a>ODBC 驅動程式架構
驅動程式撰寫者必須知道驅動程式架構，可能會影響是否應用程式可以使用 DBMS 專屬 SQL。  
  
 ![顯示 ODBC 驅動程式架構](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [以檔案為基礎的驅動程式](../../../odbc/reference/file-based-drivers.md)  
  
 當驅動程式可直接存取實體的資料時，此驅動程式會做為驅動程式和資料來源。 驅動程式必須處理呼叫 ODBC 和 SQL 陳述式。 以檔案為基礎的驅動程式的開發人員必須撰寫自己的資料庫引擎。  
  
 [以 DBMS 為基礎的驅動程式](../../../odbc/reference/dbms-based-drivers.md)  
  
 若要存取實體的資料使用不同的資料庫引擎時，驅動程式處理只 ODBC 呼叫。 傳遞 SQL 陳述式至 database engine 的處理。  
  
 [網路架構](../../../odbc/reference/network-example.md)  
  
 檔案和 DBMS ODBC 組態可以位於單一網路。  
  
 [其他驅動程式架構](../../../odbc/reference/other-driver-architectures.md)  
  
 當驅動程式需要使用各種資料來源時，它可用來當做中介軟體。 異質性聯結引擎架構可以讓驅動程式會顯示為驅動程式管理員。 驅動程式也可以安裝在伺服器上，由一系列的用戶端會共用。  
  
 如需驅動程式架構的詳細資訊，請參閱[驅動程式管理員](../../../odbc/reference/the-driver-manager.md)和[驅動程式架構](../../../odbc/reference/driver-architecture.md)上節[ODBC 架構](../../../odbc/reference/odbc-architecture.md)。  
  
 可以找到驅動程式問題的詳細資訊，在下表中所述的位置。  
  
|問題|主題|位置|  
|-----------|-----------|--------------|  
|應用程式與驅動程式相容性問題|[應用程式/驅動程式相容性](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[程式設計考量](../../../odbc/reference/develop-app/programming-considerations.md)，在 ODBC 程式設計人員參考|  
|寫入 ODBC 驅動程式|[撰寫 ODBC 3.x 驅動程式](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[程式設計考量](../../../odbc/reference/develop-app/programming-considerations.md)，在 ODBC 程式設計人員參考|  
|驅動程式的回溯相容性的指導方針|[驅動程式的回溯相容性的指導方針](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[附錄 g： 驅動程式的指導方針回溯相容性](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)，在 ODBC 程式設計人員參考|  
|連接至驅動程式|[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|[連接到資料來源或驅動程式](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)，在 ODBC 程式設計人員參考|  
|識別驅動程式|[檢視驅動程式](../../../odbc/admin/viewing-drivers.md)|[檢視驅動程式](../../../odbc/admin/viewing-drivers.md)，Microsoft ODBC 資料來源管理員線上說明|  
|啟用連線共用|[ODBC 連接共用](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|[連接到資料來源或驅動程式](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)，在 ODBC 程式設計人員參考|  
|Unicode/ANSI 驅動程式和連線問題|[Unicode 驅動程式](../../../odbc/reference/develop-app/unicode-drivers.md)|[程式設計考量](../../../odbc/reference/develop-app/programming-considerations.md)，在 ODBC 程式設計人員參考|  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
