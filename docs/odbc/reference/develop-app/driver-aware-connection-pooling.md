---
title: 驅動程式感知連接池 |微軟文件
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
ms.openlocfilehash: 70b70c841f37bd69179137c807c0dadcfd932d2b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287598"
---
# <a name="driver-aware-connection-pooling"></a>可感知驅動程式的連接共用
驅動程式感知連接池是 Windows 8 中的驅動程式管理器的新功能。 驅動程式感知連接池允許驅動程式編寫器在其ODBC驅動程式中自定義連接池行為。  
  
> [!NOTE]  
>  游標庫不支援驅動程式感知連接池。 如果應用程式嘗試透過 SQLSetConnectAttr 啟用游標庫,則應用程式在啟用驅動程式感知連接池時將收到錯誤訊息。  
  
 驅動程式感知連接池解決了與驅動程式管理員連接池相關的以下問題:  
  
 **池碎片**驅動程式管理員僅從池中返回連接,如果它與新連接請求的連接字串完全匹配。  驅動程式管理員需要完全匹配的一個原因是驅動程式管理員不瞭解每個特定於驅動程式的連接字串關鍵字及其值。  但是,某些連接字串關鍵字值(如資料庫的名稱)可能不需要完全匹配,因為驅動程式可以在不到打開新連接所需的時間內更改資料庫(確切的時差取決於數據源)。 而且,某些連接屬性(如SQL_ATTR_CURRENT_CATALOG)的差異可能需要比其他屬性(如SQL_ATTR_LOGIN_TIMEOUT)的差異更多的時間來更改。 這也可以阻止驅動程式管理器使用池中成本最低的可重用連接。 當驅動程式必須創建許多新連接時,應用程式的性能可能會降低,數據源的可伸縮性也會降低。 通過驅動程式感知連接池可以減少池碎片,因為驅動程式可以更好地估計在池中重用連接請求的成本。  
  
 **不考慮申請偏好**某些數據源可以有效地打開新連接(與重置某些屬性相比),因此,應用程式可能更喜歡打開新連接,而不是嘗試從池中重用稍微不匹配的連接並重置某些值(儘管在連接池初始化短語中這可能較慢)。 但是,某些應用程式可能會使伺服器負載變小,打開較少的連接,儘管修復不匹配的正確行為的成本可能更大。 如果沒有驅動程式感知連接池,則無法有效地指定此類首選項,因為驅動程式管理器無法識別所有特定於驅動程式的連接屬性。 驅動程式感知連接池允許驅動程式獲取使用者首選項(具有 SQLSetConnect Attr 的特定於驅動程式的屬性),以便根據使用者的首選項更好地估計從池中重用連接的成本。  
  
 關於驅動程式感知連線池的詳細資訊,請參閱[在 ODBC 驅動程式中開發連接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
## <a name="determining-driver-support"></a>確定驅動程式支援  
 驅動程式感知連接池是驅動程式可能不支援的可選功能。 要確定驅動程式是否支援它,請使用[SQL_DRIVER_AWARE_POOLING_SUPPORTED SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)*的資訊類型*。  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>如何開啟驅動程式感知連接池  
 應用程式可以通過將SQL_ATTR_CONNECTION_POOLING屬性設置為使用[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)SQL_CP_DRIVER_AWARE來使用驅動程式的連接池感知。 如果驅動程式不支援連接池感知,將使用驅動程式管理器連接池(與指定SQL_CP_ONE_PER_HENV相同,而不是SQL_CP_DRIVER_AWARE)。 ODBC 2.x 和 3.x 應用程式可以啟用此功能。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
