---
title: "可感知驅動程式的連接共用 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bf5c6405d4492a4cf559c3a62f53f69eb8a3fdeb
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="driver-aware-connection-pooling"></a>可感知驅動程式的連接共用
驅動程式可感知連接共用是 Windows 8 中的驅動程式管理員的新功能。 驅動程式可感知連接共用允許驅動程式撰寫者自訂連接共用其 ODBC 驅動程式中的行為。  
  
> [!NOTE]  
>  資料指標程式庫不支援驅動程式可感知連接共用。 如果它嘗試啟用 SQLSetConnectAttr，透過資料指標程式庫的驅動程式可感知連接共用已啟用時，應用程式會收到錯誤訊息。  
  
 驅動程式的了解連接共用位址與驅動程式管理員連線集區相關的下列問題：  
  
 **集區片段**驅動程式管理員只會傳回連接集區中是否與新的連接要求的連接字串完全相符。  為需要完全相符的驅動程式管理員的其中一個原因是，驅動程式管理員不了解每個驅動程式特有的連接字串關鍵字和其值。  不過，某些連接字串關鍵字值的 （例如資料庫的名稱） 可能不需要完全相符，因為驅動程式可以變更都不開啟新連接 （取決於資料來源的確切時間差異） 所需的時間超過資料庫。 此外，某些屬性 （例如 SQL_ATTR_CURRENT_CATALOG) 的連接屬性的差異可能需要更多的時間，若要變更其他屬性 （例如 SQL_ATTR_LOGIN_TIMEOUT) 中的差異比。 也可能會使驅動程式管理員無法從集區使用的最低成本、 可重複使用的連接。 當建立許多新的連接具有驅動程式時，可能會降低應用程式的效能，可能會降低資料來源延展性。 使用可感知驅動程式的連接共用，因為驅動程式可以進一步預估重複使用的連接集區的連線要求中的成本，可降低集區片段。  
  
 **應用程式喜好設定的任何考量**某些資料來源可以有效率地開啟新連接 （相較於某些屬性重設），因此，應用程式可能會想要開啟新連接，而不是嘗試重複使用稍微不相符從集區和某些值 （雖然這可能會變慢時連接集區初始化片語） 重設連接。 但有些應用程式可能會讓伺服器負載較小，然後開啟較少的連線，雖然可能會有更大的成本，修正為正確的行為不相符。 沒有可感知驅動程式的連線集區，您無法指定這種喜好設定有效，因為驅動程式管理員無法辨識的所有驅動程式特有的連接屬性。 可感知驅動程式的連接共用允許驅動程式，以取得 （具有 SQLSetConnectAttr 驅動程式特有屬性） 的使用者喜好設定，讓它可以進一步估計的成本，重複使用來自集區根據使用者的喜好設定的連接。  
  
 如需有關可感知驅動程式的連接共用的詳細資訊，請參閱[開發 ODBC 驅動程式中的連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
## <a name="determining-driver-support"></a>判斷驅動程式支援  
 可感知驅動程式的連接共用是驅動程式可能不支援的選用功能。 若要判斷驅動程式支援它，請使用 SQL_DRIVER_AWARE_POOLING_SUPPORTED*資訊類型*的[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>如何啟用可感知驅動程式的連接共用  
 應用程式可以使用驅動程式的連接共用感知的 SQL_ATTR_CONNECTION_POOLING 屬性設為與 SQL_CP_DRIVER_AWARE [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。 如果驅動程式不支援連接集區感知，驅動程式管理員連接共用將會使用 （如同 SQL_CP_ONE_PER_HENV 如同已指定，而不是 SQL_CP_DRIVER_AWARE 相同）。 ODBC 2.x 及 3.x 應用程式可以啟用這項功能。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)

