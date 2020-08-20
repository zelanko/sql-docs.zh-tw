---
description: 相容性矩陣
title: 相容性矩陣 |Microsoft Docs
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
ms.openlocfilehash: bafe3d85e1f4dc1c18acb057fe8c00e4ca0b36d0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461560"
---
# <a name="compatibility-matrix"></a>相容性矩陣
下表說明此區段先前定義的應用程式類型和驅動程式的相容性。  
  
|應用程式類型<br /><br /> 和版本|32位 ODBC<br /><br /> 2.x*驅動程式*|ODBC *3.x*<br /><br /> 司機|ODBC 3.8 驅動程式|ISO 和開放式群組相容驅動程式|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|16位應用程式，任何版本|相容|相容|相容|相容|  
|純粹 *2.x* 應用程式|相容|相容|相容|不相容 [3]|  
|單純 *的* 2.x 重新編譯應用程式|相容|相容 [1]|相容 [1]|不相容 [3]|  
|純粹 *2.X* Unicode 應用程式|相容|相容 [1]|相容 [1]|不相容 [3]|  
|純開放式群組和符合 ISO 規範的應用程式|不相容|相容 [2]|相容 [2]|相容 [2]|  
|純3.0 應用程式|不相容|相容|相容|不相容 [4]|  
|純3.5 應用程式|不相容|相容|相容|不相容 [4]|  
|純 3.8 (或更高的) 應用程式|不相容 [5]|不相容 [5]|相容|不相容 [4]|  
|取代的應用程式|相容|相容|相容|不相容 [3]|  
  
 [1] 如果應用程式是 Unicode 應用程式) 且必須將 ODBCVER 設定為0x0250，則應用程式必須使用 ODBC 3.5 (或更高版本的) 標 (頭重新編譯。  
  
 [2] 應用程式必須使用 ODBC 3.5 (或更高的) 標頭進行編譯，並與 ODBC 驅動程式管理員連結。 它也必須將標頭旗標設定 ODBC_STD。  
  
 [3] 此設定可能無法運作， *因為 ODBC 2.x 中的功能* 不在標準中，例如書簽。  
  
 [4] 此設定可能無法運作， *因為 ODBC 3.x 中的功能* 不在標準中，例如書簽。  
  
 [5] 這項設定可能會失敗，因為 odbc 3.8 中的功能不在 odbc 2.x 或3.x 驅動程式中，例如 ODBC 中的驅動程式特定 [C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
## <a name="driver-manager-compatibility"></a>驅動程式管理員相容性  
 必須搭配所有驅動程式管理員版本操作的 ODBC 3.0 應用程式，應該在啟動時執行下列動作：  
  
-   配置環境控制碼。  
  
-   將 SQL_ATTR_ODBC_VERSION 環境屬性設定為 SQL_OV_ODBC3_80。 如果驅動程式管理員傳回 SQL_ERROR，驅動程式管理員會早于3.8。 視需要將 SQL_ATTR_ODBC_VERSION 重設為 SQL_OV_ODBC3 或 SQL_OV_ODBC2，以對應至驅動程式管理員。  
  
-   配置連接控制碼。  
  
-   建立連接。  
  
-   針對 SQL_DRIVER_ODBC_VER 呼叫 SQLGetInfo，以判斷驅動程式版本。 如果驅動程式是 ODBC 3.8 驅動程式，您可以使用驅動程式特定的 C 類型。 否則，請勿使用驅動程式特定的 C 資料類型。  
  
 請注意，重新編譯的 ODBC 3.x 應用程式可以使用驅動程式專屬 C 類型以外的 ODBC 3.8 功能，而不需指定 SQL_ATTR_ODBC_VERSION 的 SQL_OV_ODBC3_80。 這類似于使用 ODBC 3.x 功能重新編譯的 ODBC 2.x 應用程式。  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>在與所有驅動程式管理員相容的應用程式中使用 SQLCancelHandle  
 因為在 Windows 7 之前發行的驅動程式管理員中不支援 [SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 函式，所以如果應用程式直接呼叫 **SQLCancelHandle** ，就無法在舊版 windows 中載入。 若要使用所有版本的驅動程式管理員，並在新的 Windows 版本上使用**SQLCancelHandle** ，應用程式應該使用**LoadLibrary**和 GetProcAddress 來間接呼叫**SQLCancelHandle** **。**  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 3.8 的新功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
