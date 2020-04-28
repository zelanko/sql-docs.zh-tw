---
title: 驅動程式特定的連接資訊 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConnect function [ODBC], driver-specific connection information
- connecting to driver [ODBC], SQLConnect
- SQLDriverConnect function [ODBC], driver specific connection information
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SQLConnect
- connecting to driver [ODBC], driver-specific information
ms.assetid: 3748758a-f16a-4f3b-9c40-06f2e300704e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16c8c5fc4fd3ac63aa3613b41e530446dffec118
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305787"
---
# <a name="driver-specific-connection-information"></a>特定驅動程式的連線資訊
**SQLConnect**會假設資料來源名稱、使用者識別碼和密碼足以連接至資料來源，而且所有其他連接資訊都可以儲存在系統上。 這種情況通常不會發生。 例如，驅動程式可能需要一個使用者識別碼和密碼來登入伺服器，並使用不同的使用者識別碼和密碼來登入 DBMS。 因為**SQLConnect**會接受單一使用者識別碼和密碼，這表示如果要使用**SQLConnect** ，則其他使用者識別碼和密碼必須與系統上的資料來源資訊一起儲存。 這是潛在的安全性缺口，除非密碼已加密，否則應予以避免。  
  
 **SQLDriverConnect**可讓驅動程式在連接字串的關鍵字-值組中定義任意數量的連接資訊。 例如，假設驅動程式需要資料來源名稱、伺服器的使用者識別碼和密碼，以及 DBMS 的使用者識別碼和密碼。 一律使用 XYZ Corp 資料來源的自訂程式可能會提示使用者提供識別碼和密碼，並建立下列的關鍵字-值組或*連接字串，* 以傳遞至**SQLDriverConnect**：  
  
> [!NOTE]  
>  如果您要連接到支援 Windows 驗證的資料來源提供者，您應該在`Trusted_Connection=yes`連接字串中指定而不是使用者識別碼和密碼資訊。  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 **DSN** （資料來源名稱）關鍵字會將資料來源命名為， **UID**和**PWD**關鍵字會指定伺服器的使用者識別碼和密碼，而**UIDDBMS**和**PWDDBMS**關鍵字會指定 DBMS 的使用者識別碼和密碼。 請注意，最後一個分號是選擇性的。 **SQLDriverConnect**會剖析這個字串;會使用 XYZ Corp 資料來源名稱來抓取系統中的其他連接資訊，例如伺服器位址。並使用指定的使用者識別碼和密碼登入伺服器和 DBMS。  
  
 **SQLDriverConnect**中的關鍵字-值配對必須遵循特定的語法規則。 關鍵字和其值不應包含 **[]{}（）、;？= \*！ @** 字元。 **DSN**關鍵字的值不能只包含空格，且不應包含開頭空白。 由於登錄文法的原因，關鍵字和資料來源名稱不能包含反斜線\\（）字元。 關鍵字-值組的等號前後不能有空格。  
  
 **FILEDSN**關鍵字可以在**SQLDriverConnect**的呼叫中用來指定包含資料來源資訊的檔案名（請參閱本節稍後的使用檔案[資料來源連接](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)）。 **SAVEFILE**關鍵字可以用來指定 dsn 檔案的名稱，在此檔案中，將會儲存對**SQLDriverConnect**的呼叫所進行的成功連線的關鍵字-值配對。 如需有關檔案資料來源的詳細資訊，請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函數描述。
