---
title: 可感知驅動程式的連線集區 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ea4643354990ad416ac3975467c5991842adacc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62658253"
---
# <a name="driver-aware-connection-pooling"></a>可感知驅動程式的連接共用
驅動程式知道的連接共用是在 Windows 8 中的驅動程式管理員的新功能。 驅動程式可感知連接共用，可讓自訂連接共用行為，其 ODBC 驅動程式中的驅動程式寫入器。  
  
> [!NOTE]  
>  資料指標程式庫不支援驅動程式可感知連接共用。 如果它嘗試啟用 SQLSetConnectAttr，透過資料指標程式庫所啟用的驅動程式可感知連接共用時，應用程式會收到錯誤訊息。  
  
 驅動程式知道連線集區位址驅動程式管理員連接共用與下列問題：  
  
 **集區片段**驅動程式管理員只會傳回連接集區中是否完全符合新的連線要求的連接字串。  要求完全相符的驅動程式管理員的其中一個原因是，驅動程式管理員不了解每個驅動程式特有的連接字串關鍵字和其值。  不過，某些連接字串關鍵字值的 （例如資料庫的名稱） 可能不需要完全相符，因為驅動程式可以變更的資料庫，都不超過開啟新的連接 （取決於資料來源的確切時間差異） 所需的時間。 而且，有些 （例如 SQL_ATTR_CURRENT_CATALOG) 的連接屬性中的差異可能需要更多的時間比其他屬性 （例如 SQL_ATTR_LOGIN_TIMEOUT) 中的差異變更。 這項目，也可以防止驅動程式管理員從集區使用的最低成本、 可重複使用的連接。 當驅動程式需要建立許多新的連線時，應用程式的效能可能會降低，可能會降低資料來源的延展性。 使用可感知驅動程式的連接共用，因為驅動程式可以更精確地預估的成本重複使用連線要求的集區中的連接，可降低集區片段。  
  
 **應用程式喜好設定的任何考量**某些資料來源可以有效率地開啟新連接 （相較於重設某些屬性），因此，應用程式可能會想要開啟新的連接，而不是嘗試重複使用稍有不相符從集區和某些值 （雖然這可能會變慢時連接集區初始化片語） 重設連接。 但是有些應用程式可能會保持較小的伺服器負載，然後開啟較少的連線，雖然可能會有更大的成本，若要修正針對正確的行為不相符。 沒有可感知驅動程式的連線集區，您無法指定這種喜好設定有效，因為驅動程式管理員不會辨識所有的驅動程式特有的連接屬性。 可感知驅動程式的連接共用，可讓驅動程式，即可取得 （使用 SQLSetConnectAttr 驅動程式特有屬性） 的使用者喜好設定，以便它可以更精確地預估的成本重複使用從根據使用者的喜好設定的集區的連線。  
  
 如需有關可感知驅動程式的連接共用的詳細資訊，請參閱 < [ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
## <a name="determining-driver-support"></a>判斷驅動程式支援  
 可感知驅動程式的連接共用是驅動程式可能不支援的選擇性功能。 若要判斷驅動程式支援它，請使用 SQL_DRIVER_AWARE_POOLING_SUPPORTED*資訊類型*的[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>如何啟用可感知驅動程式的連接共用  
 應用程式可以使用驅動程式的連接共用感知的 SQL_ATTR_CONNECTION_POOLING 屬性設為與 SQL_CP_DRIVER_AWARE [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。 如果驅動程式不支援連接集區覺察，驅動程式管理員連接共用將會使用 （如同已指定 SQL_CP_ONE_PER_HENV，而不是 SQL_CP_DRIVER_AWARE 相同）。 ODBC 2.x 及 3.x 應用程式可啟用這項功能。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
