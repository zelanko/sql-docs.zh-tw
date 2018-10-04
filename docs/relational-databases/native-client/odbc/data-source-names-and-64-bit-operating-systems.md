---
title: 資料來源名稱和 64 位元作業系統 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: c2f86810-2775-4ddd-8df7-e8373785a7fc
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2248077b8efed3ebf11f871603a6513d6b9f4a02
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47612563"
---
# <a name="data-source-names-and-64-bit-operating-systems"></a>資料來源名稱和 64 位元作業系統
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  若要建立並執行應用程式，當做 64 位元作業系統上的 32 位元應用程式，您必須利用 %windir%\SysWOW64\odbcad32.exe，以 ODBC 管理員身分建立 ODBC 資料來源。  
  
## <a name="remarks"></a>備註  
 64 位元的 Windows 作業系統有兩個 odbcad32.exe 檔案：  
  
-   %SystemRoot%\system32\odbcad32.exe 用於建立與維持 64 位元應用程式的資料來源名稱。  
  
-   %SystemRoot%\SysWOW64\odbcad32.exe 用於建立與維持 32 位元應用程式的資料來源名稱，包括在 64 位元作業系統上執行的 32 位元應用程式。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
