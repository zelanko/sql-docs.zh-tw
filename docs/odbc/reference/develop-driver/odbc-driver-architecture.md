---
title: ODBC 驅動程式架構 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], architecture
ms.assetid: 21a62c7c-192e-4718-a16e-aa12b0de4419
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 260767c88fdf980466a21d4cc9658b259b91c854
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47788146"
---
# <a name="odbc-driver-architecture"></a>ODBC 驅動程式架構
驅動程式撰寫者必須注意是否應用程式可以使用的 DBMS 特定 SQL 驅動程式架構可能會影響。  
  
 ![顯示 ODBC 驅動程式架構](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [檔案為基礎的驅動程式](../../../odbc/reference/file-based-drivers.md)  
  
 當驅動程式會直接存取實體的資料時，此驅動程式會作為驅動程式和資料來源。 驅動程式必須處理呼叫 ODBC 和 SQL 陳述式。 檔案為基礎的驅動程式的開發人員必須撰寫自己的資料庫引擎。  
  
 [以 DBMS 為基礎的驅動程式](../../../odbc/reference/dbms-based-drivers.md)  
  
 當個別的資料庫引擎用來存取實體的資料時，驅動程式會處理僅 ODBC 呼叫。 它會傳遞 SQL 陳述式給資料庫引擎進行處理。  
  
 [網路架構](../../../odbc/reference/network-example.md)  
  
 檔案和 DBMS ODBC 組態可以有單一的網路。  
  
 [其他驅動程式架構](../../../odbc/reference/other-driver-architectures.md)  
  
 當驅動程式，才能使用各種資料來源時，它可用來當做中介軟體。 異質性聯結引擎架構可讓驅動程式會顯示為驅動程式管理員。 也可以在伺服器上，由一系列的用戶端會共用安裝驅動程式。  
  
 如需有關驅動程式架構的詳細資訊，請參閱[驅動程式管理員](../../../odbc/reference/the-driver-manager.md)並[驅動程式架構](../../../odbc/reference/driver-architecture.md)上一節[ODBC 架構](../../../odbc/reference/odbc-architecture.md)。  
  
 可以找到驅動程式問題的詳細資訊，在下表中所述的位置。  
  
|問題|主題|位置|  
|-----------|-----------|--------------|  
|應用程式與驅動程式的相容性問題|[應用程式/驅動程式相容性](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[程式設計考量](../../../odbc/reference/develop-app/programming-considerations.md)，在 ODBC 程式設計人員參考|  
|撰寫 ODBC 驅動程式|[撰寫 ODBC 3.x 驅動程式](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[程式設計考量](../../../odbc/reference/develop-app/programming-considerations.md)，在 ODBC 程式設計人員參考|  
|為了與舊版相容的驅動程式指導方針|[為了與舊版相容的驅動程式指導方針](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[附錄 g： 回溯相容性的驅動程式指導方針](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)，在 ODBC 程式設計人員參考|  
|連接到驅動程式|[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|[連接至資料來源或驅動程式](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)，在 ODBC 程式設計人員參考|  
|找出驅動程式|[檢視驅動程式](../../../odbc/admin/viewing-drivers.md)|[檢視驅動程式](../../../odbc/admin/viewing-drivers.md)，在 Microsoft ODBC 資料來源管理員線上說明|  
|啟用連線共用|[ODBC 連接共用](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|[連接至資料來源或驅動程式](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)，在 ODBC 程式設計人員參考|  
|Unicode/ANSI 驅動程式和連線問題|[Unicode 驅動程式](../../../odbc/reference/develop-app/unicode-drivers.md)|[程式設計考量](../../../odbc/reference/develop-app/programming-considerations.md)，在 ODBC 程式設計人員參考|  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
