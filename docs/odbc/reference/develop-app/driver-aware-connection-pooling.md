---
description: 可感知驅動程式的連接共用
title: 驅動程式感知連接共用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed2fa29a68095be9cfcc7d4192c6dc2e15f3eac7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494656"
---
# <a name="driver-aware-connection-pooling"></a>可感知驅動程式的連接共用
驅動程式感知連接共用是 Windows 8 中驅動程式管理員的新功能。 驅動程式感知連接共用可讓驅動程式寫入器自訂其 ODBC 驅動程式中的連接共用行為。  
  
> [!NOTE]  
>  資料指標程式庫不支援驅動程式感知連接共用。 當啟用驅動程式感知連接共用時，如果應用程式嘗試透過 SQLSetConnectAttr 啟用資料指標程式庫，則會收到錯誤訊息。  
  
 驅動程式感知連接共用可解決下列與驅動程式管理員連接共用相關的問題：  
  
 **集區片段** 驅動程式管理員只會在與新連線要求的連接字串完全相符時，才會從集區傳回連接。  驅動程式管理員需要完全相符的原因之一，就是驅動程式管理員不了解每個驅動程式特定的連接字串關鍵字和其值。  不過，某些連接字串關鍵字值 (例如資料庫的名稱) 可能不需要完全相符，因為驅動程式可能會在開啟新連接所需的時間內變更資料庫 (確切的時間差異取決於資料來源) 。 此外，某些連接屬性 (例如 SQL_ATTR_CURRENT_CATALOG) 的差異，可能需要更多的時間來變更，而不像其他屬性 (的差異，例如 SQL_ATTR_LOGIN_TIMEOUT) 。 如此一來，就可以防止驅動程式管理員使用來自集區的最低成本、可重複使用的連接。 當驅動程式必須建立許多新的連接時，應用程式的效能可能會降低，而且資料來源的擴充性可能會降低。 您可以使用驅動程式感知的連接共用來減少集區片段，因為驅動程式可以更有效地估計在集區中重複使用連線要求的連接成本。  
  
 **不考慮應用程式喜好** 設定某些資料來源可以有效率地開啟新的連接 (相較于重設某些屬性) ，因此，應用程式可能會偏好開啟新的連接，而不是嘗試重複使用與集區稍微不相符的連接，並重設一些值 (不過，在連接集區初始化片語) 期間，這可能會比較慢。 但是，有些應用程式可能會讓伺服器負載變得較小，而且會開啟較少的連線，不過修正不相符的問題可能會有較大的成本來修正。 若沒有可感知驅動程式的連接共用，您就無法有效指定這種喜好設定，因為驅動程式管理員無法辨識所有驅動程式特定的連接屬性。 可感知驅動程式的連線共用可讓驅動程式使用 SQLSetConnectAttr) 的驅動程式專屬屬性來取得使用者喜好設定 (，讓它可以根據使用者的喜好設定，以更好的方式預估從集區中重複使用連線的成本。  
  
 如需驅動程式感知連接共用的詳細資訊，請參閱 [在 ODBC 驅動程式中開發連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
## <a name="determining-driver-support"></a>判斷驅動程式支援  
 驅動程式感知連接共用是驅動程式可能不支援的選用功能。 若要判斷驅動程式是否支援該驅動程式，請使用 SQL_DRIVER_AWARE_POOLING_SUPPORTED *InfoType* of [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>如何啟用驅動程式感知連接共用  
 應用程式可以使用 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)將 SQL_ATTR_CONNECTION_POOLING 屬性設定為 SQL_CP_DRIVER_AWARE，藉此使用驅動程式的連線共用感知。 如果驅動程式不支援連接集區感知，則會使用驅動程式管理員連接共用 (與 SQL_CP_ONE_PER_HENV 已指定的相同，而不是 SQL_CP_DRIVER_AWARE) 。 ODBC 2.x 和3.x 應用程式可以啟用這項功能。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
