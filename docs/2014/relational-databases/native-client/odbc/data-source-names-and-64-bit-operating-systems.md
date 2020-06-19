---
title: 資料來源名稱和64位作業系統 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: c2f86810-2775-4ddd-8df7-e8373785a7fc
author: rothja
ms.author: jroth
ms.openlocfilehash: ae31584ca3c076919f688d1ef9bdef80706c6940
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055849"
---
# <a name="data-source-names-and-64-bit-operating-systems"></a>資料來源名稱和 64 位元作業系統
  若要建立並執行應用程式，當做 64 位元作業系統上的 32 位元應用程式，您必須利用 %windir%\SysWOW64\odbcad32.exe，以 ODBC 管理員身分建立 ODBC 資料來源。  
  
## <a name="remarks"></a>備註  
 64 位元的 Windows 作業系統有兩個 odbcad32.exe 檔案：  
  
-   %SystemRoot%\system32\odbcad32.exe 用於建立與維持 64 位元應用程式的資料來源名稱。  
  
-   %SystemRoot%\SysWOW64\odbcad32.exe 用於建立與維持 32 位元應用程式的資料來源名稱，包括在 64 位元作業系統上執行的 32 位元應用程式。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
