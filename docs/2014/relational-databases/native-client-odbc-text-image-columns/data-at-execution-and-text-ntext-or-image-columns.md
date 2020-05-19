---
title: 資料執行中和 Text、Ntext 或 Image 資料行 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- data-at-execution
- ODBC data-at-execution
- image columns [ODBC]
ms.assetid: 67ffb1a6-f38d-4712-ba64-96bdd41ec2b2
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4368104ffcad31a59bfa1a3acffb38fcd015156e
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718848"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>資料執行中和 Text、ntext 或 Image 資料行
  ODBC 資料執行中是一種功能，可讓應用程式針對繫結的資料行或參數使用相當大量的資料。 當您抓取非常大的**text**、 **Ntext**或**image**資料行時，應用程式可能無法只配置大型緩衝區、將資料行系結至緩衝區，以及提取資料列。 更新非常大的**text**、 **Ntext**或**image**資料行時，應用程式可能無法只配置大型緩衝區、將它系結至 SQL 語句中的參數標記，然後執行語句。 在這些情況下，應用程式必須使用[SQLGetData](../native-client-odbc-api/sqlgetdata.md)或[SQLPutData](../native-client-odbc-api/sqlputdata.md)搭配其資料執行中選項。  
  
## <a name="see-also"></a>另請參閱  
 [管理 Text 和 Image 資料行](managing-text-and-image-columns.md)  
  
  
