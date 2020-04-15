---
title: 相容性矩陣 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0406599e1657a900d1669861572ff13834cec670
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307451"
---
# <a name="compatibility-matrix"></a>相容性矩陣
下表描述了本節中前面定義的應用程式和驅動程式類型的相容性。  
  
|應用程式類型<br /><br /> 和版本|32 位元 ODBC<br /><br /> *2.x*驅動程式|ODBC *3.x*<br /><br /> 司機|ODBC 3.8 驅動程式|符合 ISO 與開啟群組的驅動程式|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|16 位元應用程式,任何版本|相容|相容|相容|相容|  
|純*2.x*應用|相容|相容|相容|不相容[3]|  
|純*2.x*重新編譯的應用程式|相容|相容[1]|相容[1]|不相容[3]|  
|純*2.x* Unicode 應用程式|相容|相容[1]|相容[1]|不相容[3]|  
|純開放群組和符合 ISO 的應用程式|不相容|相容[2]|相容[2]|相容[2]|  
|純 3.0 應用|不相容|相容|相容|不相容[4]|  
|純 3.5 應用|不相容|相容|相容|不相容[4]|  
|純 3.8(或更高)應用|不相容 [5]|不相容 [5]|相容|不相容 [4]|  
|取代應用程式|相容|相容|相容|不相容[3]|  
  
 [1] 應用程式必須使用具有 UNICODE 選項(如果是 Unicode 應用程式)的 ODBC 3.5(或更高)標頭重新編譯,並且必須將 ODBCVER 設置為 0x0250。  
  
 [2] 應用程式必須使用 ODBC 3.5(或更高)標頭進行編譯,並與 ODBC 驅動程式管理器連結。 它還必須ODBC_STD設置標題標誌。  
  
 [3] 此配置可能不起作用,因為 ODBC *2.x*中有些功能不在標準中,例如書籤。  
  
 [4] 此配置可能不起作用,因為 ODBC *3.x*中有些功能不在標準中,例如書籤。  
  
 [5] 此設定可能會失敗,因為 ODBC 3.8 中有些功能不在 ODBC 2.x 或 3.x 驅動程式中,例如[ODBC 中](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)特定於驅動程式的 C 資料類型。  
  
## <a name="driver-manager-compatibility"></a>驅動程式管理員相容性  
 必須在所有驅動程式管理器版本操作的 ODBC 3.0 應用程式應在啟動時執行以下操作:  
  
-   分配環境句柄。  
  
-   將SQL_ATTR_ODBC_VERSION環境屬性設置為SQL_OV_ODBC3_80。 如果驅動程式管理器返回SQL_ERROR,則驅動程式管理器大於 3.8。 根據需要將SQL_ATTR_ODBC_VERSION重置為SQL_OV_ODBC3或SQL_OV_ODBC2,以便與驅動程式管理器相對應。  
  
-   分配連接句柄。  
  
-   建立連接。  
  
-   呼叫 SQLGetInfo 進行SQL_DRIVER_ODBC_VER以確定驅動程式版本。 如果驅動程式是 ODBC 3.8 驅動程式,則可以使用特定於驅動程式的 C 類型。 否則,不要使用特定於驅動程式的 C 數據類型。  
  
 請注意,重新編譯的 ODBC 3.x 應用程式可以使用特定於驅動程式的 C 類型以外的 ODBC 3.8 功能,而無需為SQL_ATTR_ODBC_VERSION指定SQL_OV_ODBC3_80。 這與使用 ODBC 3.x 功能重新編譯的 ODBC 2.x 應用程式類似。  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>在與所有驅動程式管理員相容的應用程式中使用 SQLCancelHandle  
 由於在 Windows 7 之前發布的驅動程式管理器中不支援[SQLCancelHandle 函數](../../../odbc/reference/syntax/sqlcancelhandle-function.md),因此如果應用程式直接呼叫**SQLCancelHandle,** 則無法在舊版本的 Windows 中載入它。 要使用所有版本的驅動程式管理器並在新版本的 Windows 上使用**SQLCancelHandle,** 應用程式應使用**LoadLibrary**和**GetProcAddress**間接調用**SQLCancelHandle。**  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 3.8 的新功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
