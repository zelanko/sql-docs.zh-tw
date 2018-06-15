---
title: 相容性比較表 |Microsoft 文件
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
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application compatibility issues [ODBC]
- application upgrades [ODBC], compatibility matrix
- upgrading applications [ODBC], compatibility matrix
ms.assetid: 0690b463-15a1-48fa-9d0b-9cc9e5bf7fc6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09f09d5a8b6e15c677969b2b865e3908200108e4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32912433"
---
# <a name="compatibility-matrix"></a>相容性比較表
下表描述的相容性的應用程式和驅動程式，本節先前定義的類型。  
  
|應用程式類型<br /><br /> 和版本|32 位元 ODBC<br /><br /> 2.*x*驅動程式|ODBC 3。*x*<br /><br /> 驅動程式|ODBC 3.8 驅動程式|ISO 和相容開啟群組的驅動程式|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|16 位元應用程式中，任何版本|相容|相容|相容|相容|  
|純 2。*x*應用程式|相容|相容|相容|不相容 [3]|  
|純 2。*x*重新編譯應用程式|相容|相容性 [1]|相容性 [1]|不相容 [3]|  
|純 2。*x* Unicode 應用程式|相容|相容性 [1]|相容性 [1]|不相容 [3]|  
|純的 Open Group 和 ISO 相容的應用程式|不相容|相容性 [2]|相容性 [2]|相容性 [2]|  
|純 3.0 的應用程式|不相容|相容|相容|不相容 [4]|  
|純 3.5 應用程式|不相容|相容|相容|不相容 [4]|  
|純 3.8 （或更新版本） 的應用程式|不相容 [5]|不相容 [5]|相容|不相容 [4]|  
|已取代的應用程式|相容|相容|相容|不相容 [3]|  
  
 [1] 的應用程式必須重新編譯 ODBC 3.5 （或更新版本） 標頭使用 UNICODE 選項 （如果它是在 Unicode 應用程式），必須將 ODBCVER 設 0x0250。  
  
 [2] 的應用程式必須編譯使用 ODBC 3.5 （或更新版本） 標頭，並將連結的 ODBC 驅動程式管理員。 它也必須設定標頭旗標 ODBC_STD。  
  
 [3] 這項設定可能無法運作，因為 ODBC 2 沒有功能。*x*所沒有的標準，例如書籤。  
  
 [4] 這項設定可能無法運作，因為在 ODBC 3 的功能 *.x*所沒有的標準，例如書籤。  
  
 [5] 這項設定可能會因為未在 ODBC 2.x 或 3.x 驅動程式，例如驅動程式專屬 ODBC 3.8 功能[ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
## <a name="driver-manager-compatibility"></a>驅動程式管理員相容性  
 必須在所有的驅動程式管理員版本上運作的 ODBC 3.0 應用程式應該執行上啟動下列：  
  
-   配置環境控制代碼。  
  
-   設 SQL_OV_ODBC3_80 SQL_ATTR_ODBC_VERSION 環境屬性。 如果驅動程式管理員會傳回 SQL_ERROR，驅動程式管理員比 3.8。 重設 SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3 或 SQL_OV_ODBC2，適當地對應到驅動程式管理員。  
  
-   配置連接控制代碼。  
  
-   建立連線。  
  
-   呼叫 SQLGetInfo 如 SQL_DRIVER_ODBC_VER 判斷驅動程式版本。 如果 ODBC 3.8 驅動程式的驅動程式，您可以使用特定驅動程式的 C 類型。 否則，請勿使用特定驅動程式的 C 資料類型。  
  
 請注意，重新編譯的 ODBC 3.x 應用程式可以使用 ODBC 3.8 功能以外的驅動程式特有的 C 類型但不指定為 SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3_80。 這是類似於使用 ODBC 3.x 功能的重新編譯 ODBC 2.x 應用程式。  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>在應用程式與相容的所有驅動程式管理員使用 SQLCancelHandle  
 因為[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)不支援在 Windows 7 之前發行的驅動程式管理員，應用程式無法呼叫在舊版 Windows 中載入**SQLCancelHandle**直接。 若要使用所有版本的驅動程式管理員，並使用**SQLCancelHandle**應用程式應該在新版本的 Windows，呼叫**SQLCancelHandle**利用間接**LoadLibrary**和**GetProcAddress。**  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 3.8 的新功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
