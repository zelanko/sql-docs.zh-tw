---
title: 了解資料指標類型 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4f4d3db7-4f76-450d-ab63-141237a4f034
caps.latest.revision: 51
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df4f0f6e43c0eb7184f8421d3ebeada44e74a3e4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853303"
---
# <a name="understanding-cursor-types"></a>了解資料指標類型
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  關聯式資料庫中的作業會針對完整的資料列集運作。 由 SELECT 陳述式所傳回的資料列集包括所有滿足陳述式 WHERE 子句之條件的資料列。 由陳述式傳回的完整資料列稱為結果集。 應用程式不一定能夠以一個單位有效地運用整個結果集。 這些應用程式需要一個機制，一次運用一個資料列或小型資料列區塊。 資料指標就是一種結果集的擴充，提供此種機制。  
  
 資料指標擴充結果集藉由下列方式處理：  
  
-   允許定位於結果集中的特定資料列。  
  
-   從結果集的目前位置，擷取一個資料列或資料列區塊。  
  
-   支援結果集目前位置上資料列的資料修改。  
  
-   支援以不同可見性層級來檢視其他使用者對結果集所呈現的資料庫資料所作的變更。  
  
> [!NOTE]  
>  如需完整的說明[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料指標類型，請參閱中的 < 資料指標類型 (Database Engine) > 主題[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
 JDBC 規格支援順向資料指標與可捲動的資料指標，這些資料指標可區分或無法區分其他工作所做的變更，而且可以是唯讀的或可更新的。 這項功能由[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)類別。  
  
## <a name="remarks"></a>備註  
 JDBC Driver 支援下列資料指標類型：  
  
|結果集<br /><br /> (資料指標) 類型|SQL Server 資料指標類型|特性|select<br /><br /> 方法|response<br /><br /> 緩衝|Description|  
|------------------------------------|----------------------------|---------------------|-----------------------|----------------------------|-----------------|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|해당 사항 없음|順向、唯讀|直接|完整|應用程式必須單一 (順向) 通過結果集。 這是預設的行為，而且與 TYPE_SS_DIRECT_FORWARD_ONLY 資料指標的行為相同。 驅動程式會在陳述式執行時間，將完整的結果集從伺服器讀入記憶體中。|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|해당 사항 없음|順向、唯讀|直接|adaptive|應用程式必須單一 (順向) 通過結果集。 它與 TYPE_SS_DIRECT_FORWARD_ONLY 資料指標的行為相同。 驅動程式會因為應用程式的要求而從伺服器讀取資料集，因此會將用戶端的記憶體使用量降到最低。|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|向前快轉|順向、唯讀|cursor|해당 사항 없음|應用程式必須使用伺服器資料指標單一 (順向) 通過結果集。 它與 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY 資料指標的行為相同。<br /><br /> 從伺服器中擷取資料列 (以提取大小所指定的區塊為單位)。|  
|TYPE_FORWARD_ONLY (CONCUR_UPDATABLE)|動態 (順向)|順向、可更新的|해당 사항 없음|해당 사항 없음|應用程式必須單一 (順向) 通過結果集以更新一或多個資料列。<br /><br /> 從伺服器中擷取資料列 (以提取大小所指定的區塊為單位)。<br /><br /> 根據預設，提取大小固定的應用程式進行呼叫時[setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)物件。<br /><br /> **注意：** JDBC driver 提供了適應性緩衝功能，可讓您擷取從陳述式執行結果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]應用程式需要時，而非一次。 例如，如果應用程式應該擷取的大型資料過大而無法完整納入應用程式記憶體中，適應性緩衝就會允許用戶端應用程式將這類值擷取成資料流。 驅動程式的預設行為是"**適應性**"。 不過，若要取得的順向可更新結果集的適應性緩衝，應用程式必須明確地呼叫[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)物件藉由提供**字串**值"**適應性"**。 如需範例程式碼，請參閱[更新大型資料範例](../../connect/jdbc/updating-large-data-sample.md)。|  
|TYPE_SCROLL_INSENSITIVE|靜態|可捲動、不可更新<br /><br /> 系統不會顯示外部資料列更新、插入和刪除。|해당 사항 없음|해당 사항 없음|應用程式需要資料庫快照集。 此結果集不可更新。 僅支援 CONCUR_READ_ONLY。  搭配這種資料指標類型使用時，所有其他並行類型都會導致例外狀況發生。<br /><br /> 從伺服器中擷取資料列 (以提取大小所指定的區塊為單位)。|  
|TYPE_SCROLL_SENSITIVE<br /><br /> (CONCUR_READ_ONLY)|索引鍵集|可捲動、唯讀。 系統會顯示外部資料列更新，而且刪除會顯示為遺失資料。<br /><br /> 系統不會顯示外部資料列插入。|해당 사항 없음|해당 사항 없음|應用程式必須僅針對現有的資料列查看變更的資料。<br /><br /> 從伺服器中擷取資料列 (以提取大小所指定的區塊為單位)。|  
|TYPE_SCROLL_SENSITIVE<br /><br /> (CONCUR_UPDATABLE、CONCUR_SS_SCROLL_LOCKS、CONCUR_SS_OPTIMISTIC_CC、CONCUR_SS_OPTIMISTIC_CCVAL)|索引鍵集|可捲動、可更新。<br /><br /> 系統會顯示外部和內部資料列更新，而且刪除會顯示為遺失資料，但是不會顯示插入。|해당 사항 없음|해당 사항 없음|應用程式可能使用結果集物件，以變更現有的資料列中的資料。 應用程式也必須能夠看到資料列之外的結果集物件由其他人所做的變更。<br /><br /> 從伺服器中擷取資料列 (以提取大小所指定的區塊為單位)。|  
|TYPE_SS_DIRECT_FORWARD_ONLY|해당 사항 없음|順向、唯讀|해당 사항 없음|完整或適應性|整數值 = 2003。 提供完整緩衝的唯讀用戶端資料指標。 系統不會建立任何伺服器資料指標。<br /><br /> 僅支援 CONCUR_READ_ONLY 並行類型。 搭配這種資料指標類型使用時，所有其他並行類型都會導致例外狀況發生。|  
|TYPE_SS_SERVER_CURSOR_FORWARD_ONLY|向前快轉|順向|해당 사항 없음|해당 사항 없음|整數值 = 2004。 使用伺服器資料指標來快速存取所有資料。 搭配 CONCUR_UPDATABLE 並行類型使用時，它是可更新的。<br /><br /> 從伺服器中擷取資料列 (以提取大小所指定的區塊為單位)。<br /><br /> 若要取得此案例的適應性緩衝，應用程式必須明確地呼叫[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)物件藉由提供**字串**值"**適應性"**。 如需範例程式碼，請參閱[更新大型資料範例](../../connect/jdbc/updating-large-data-sample.md)。|  
|TYPE_SS_SCROLL_STATIC|靜態|系統不會反映其他使用者的更新。|해당 사항 없음|해당 사항 없음|整數值 = 1004。 應用程式需要資料庫快照集。 這是[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-JDBC TYPE_SCROLL_INSENSITIVE 的特有同義字而且具有相同的並行設定行為。<br /><br /> 從伺服器中擷取資料列 (以提取大小所指定的區塊為單位)。|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> (CONCUR_READ_ONLY)|索引鍵集|可捲動、唯讀。 系統會顯示外部資料列更新，而且刪除會顯示為遺失資料。<br /><br /> 系統不會顯示外部資料列插入。|해당 사항 없음|해당 사항 없음|整數值 = 1005。 應用程式必須僅針對現有的資料列查看變更的資料。 這是[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-JDBC TYPE_SCROLL_SENSITIVE 的特有同義字而且具有相同的並行設定行為。<br /><br /> 從伺服器中擷取資料列 (以提取大小所指定的區塊為單位)。|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> (CONCUR_UPDATABLE、CONCUR_SS_SCROLL_LOCKS、CONCUR_SS_OPTIMISTIC_CC、CONCUR_SS_OPTIMISTIC_CCVAL)|索引鍵集|可捲動、可更新。<br /><br /> 系統會顯示外部和內部資料列更新，而且刪除會顯示為遺失資料，但是不會顯示插入。|해당 사항 없음|해당 사항 없음|整數值 = 1005。 應用程式必須變更資料或針對現有的資料列查看變更的資料。 這是[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-JDBC TYPE_SCROLL_SENSITIVE 的特有同義字而且具有相同的並行設定行為。<br /><br /> 從伺服器中擷取資料列 (以提取大小所指定的區塊為單位)。|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> (CONCUR_READ_ONLY)|動態|可捲動、唯讀。<br /><br /> 系統會顯示外部資料列更新和插入，而且刪除在目前的提取緩衝區中，會顯示為暫時遺失的資料。|해당 사항 없음|해당 사항 없음|整數值 = 1006。 應用程式必須針對現有的資料列查看變更的資料，並查看在資料指標存留時間期間插入以及刪除的資料列。<br /><br /> 從伺服器中擷取資料列 (以提取大小所指定的區塊為單位)。|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> (CONCUR_UPDATABLE、CONCUR_SS_SCROLL_LOCKS、CONCUR_SS_OPTIMISTIC_CC、CONCUR_SS_OPTIMISTIC_CCVAL)|動態|可捲動、可更新。<br /><br /> 系統會顯示外部和內部資料列更新和插入，而且刪除在目前的提取緩衝區中，會顯示為暫時遺失的資料。|해당 사항 없음|해당 사항 없음|整數值 = 1006。 應用程式可能會變更現有的資料列的資料或插入或刪除資料列使用結果集物件。 應用程式也必須能夠看見變更、 插入和刪除之外的結果集物件由其他人所做的動作。<br /><br /> 從伺服器中擷取資料列 (以提取大小所指定的區塊為單位)。|  
  
## <a name="cursor-positioning"></a>資料指標定位  
 TYPE_FORWARD_ONLY、 TYPE_SS_DIRECT_FORWARD_ONLY 和 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY 資料指標僅支援[下一步](../../connect/jdbc/reference/next-method-sqlserverresultset.md)定位方法。  
  
 TYPE_SS_SCROLL_DYNAMIC 資料指標不支援[絕對](../../connect/jdbc/reference/absolute-method-sqlserverresultset.md)和[getRow](../../connect/jdbc/reference/getrow-method-sqlserverresultset.md)方法。 Absolute 方法呼叫的組合近似[第一個](../../connect/jdbc/reference/first-method-sqlserverresultset.md)和[相對](../../connect/jdbc/reference/relative-method-sqlserverresultset.md)動態資料指標的方法。  
  
 TYPE_FORWARD_ONLY、 TYPE_SS_DIRECT_FORWARD_ONLY、 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY、 TYPE_SS_SCROLL_KEYSET 和 TYPE_SS_SCROLL_STATIC 資料指標只支援 getRow 方法。 具有全部順向資料指標類型的 getRow 方法，傳回目前透過資料指標讀取的資料列數目。  
  
> [!NOTE]  
>  當應用程式進行不支援的資料指標定位呼叫時或不支援的呼叫 getRow 方法時，擲回例外狀況訊息，「 要求的作業不支援使用這個資料指標類型 」。  
  
 只有 TYPE_SS_SCROLL_KEYSET 和相等的 TYPE_SCROLL_SENSITIVE 資料指標會公開已刪除的資料列。 如果游標位於已刪除的資料列，則無法使用，資料行值而[rowDeleted](../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md)方法會傳回"true"。 呼叫以取得\<類型 > 方法擲回例外狀況訊息: 「 無法從已刪除的資料列取得值 」。 無法更新已刪除的資料列。 如果您嘗試呼叫 update\<類型 > 刪除的資料列上的方法，擲回例外狀況訊息: 「 無法更新已刪除的資料列 」。 TYPE_SS_SCROLL_DYNAMIC 資料指標在移出目前的提取緩衝區之前的行為都相同。  
  
 向前資料指標和動態資料指標會以類似的方式公開已刪除的資料列，但是只有在資料指標仍可在提取緩衝區中存取時才是如此。 若是向前資料指標，這是十分簡單的。 若是動態資料指標，當提取大小大於 1 時，則比較複雜。 應用程式可以在提取緩衝區定義的視窗內前後移動資料指標，但是在遺失已更新的原始提取緩衝區時，已刪除的資料列將會消失。 如果應用程式不想使用動態資料指標查看暫時刪除的資料列，則應使用 Fetch Relative (0)。  
  
 如果 TYPE_SS_SCROLL_KEYSET 或 TYPE_SCROLL_SENSITIVE 資料指標資料列的索引鍵值隨著資料指標一起更新，不管更新的資料列是否符合資料指標的選取條件，資料列都會保留在結果集的原始位置中。 如果資料列是在資料指標外部更新，已刪除的資料列將會出現在資料列的原始位置，但是只有在具有新索引鍵值的另一個資料列在已經刪除後出現在資料指標時，資料列才會出現在資料指標中。  
  
 若是動態資料指標，更新的資料列將保留在提取緩衝區中的位置中，直到遺失提取緩衝區所定義的視窗為止。 更新的資料列後來可能會重複出現在資料集中的不同位置，也可能完全消失。 必須防止在結果集中產生暫時不一致的應用程式應該使用的提取大小為 1 (預設 CONCUR_SS_SCROLL_LOCKS 並行有 8 個資料列，而其他並行有 128 個資料列)。  
  
## <a name="cursor-conversion"></a>資料指標轉換  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 有時候可以選擇實作要求之外的資料指標類型，也就是做為隱含資料指標轉換 （或資料指標轉化）。 如需有關隱含資料指標轉換的詳細資訊，請參閱中的 < 使用隱含資料指標轉換 > 主題[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
 與[!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)]，當您更新透過 ResultSet.TYPE_SCROLL_SENSITIVE 和 ResultSet.CONCUR_UPDATABLE 結果的資料設定，會擲回例外狀況訊息 「 資料指標為 READ ONLY 」。 發生這個例外狀況，因為[!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)]已經針對該結果集，並不會傳回已經要求可更新資料指標完成隱含資料指標轉換。  
  
 若要解決這個問題，您可以執行下列其中一種解決方案：  
  
-   確保基礎資料表擁有主索引鍵。  
  
-   使用[SQLServerResultSet.TYPE_SS_SCROLL_DYNAMIC](../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md)而不是 ResultSet.TYPE_SCROLL_SENSITIVE 時建立陳述式。  
  
## <a name="cursor-updating"></a>資料指標更新  
 對於資料指標類型和並行支援更新的資料指標，支援就地更新。 如果資料指標沒有定位中結果集的可更新資料列 (沒有 get\<類型 > 方法呼叫成功)，更新呼叫\<類型 > 方法會擲回例外狀況訊息、 「 結果集有任何目前的資料列 」。 針對資料指標為 CONCUR_READ_ONLY 的資料行呼叫更新方法時，JDBC 規格會說明引發例外狀況。 在其中的資料列不是可更新，例如競相更新或刪除的開放式並行存取衝突的情況下，可能不會引發例外狀況之前[insertRow](../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md)， [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)，或[deleteRow](../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md)呼叫。  
  
 呼叫更新後\<類型 >，受影響的資料行無法存取 get\<類型 > 直到 updateRow 或[cancelRowUpdates](../../connect/jdbc/reference/cancelrowupdates-method-sqlserverresultset.md)已呼叫。 這樣可以避免使用不同於伺服器所傳回之類型更新資料行所產生的問題，而且後續的 getter 呼叫可能會叫用產生不正確結果的用戶端類型轉換。 呼叫以取得\<類型 > 將會擲回例外狀況訊息、 「 無法存取已更新的資料行，直到 updaterow （） 或 cancelrowupdates （） 之後呼叫。 」  
  
> [!NOTE]  
>  如果沒有資料行已更新時呼叫 updateRow 方法，JDBC 驅動程式將會擲回例外狀況訊息，「"已經更新任何資料行時呼叫 updaterow （）。  
  
 之後[moveToInsertRow](../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md)已呼叫，將會擲回例外狀況以外的任何方法取得\<類型 >，更新\<類型 >，insertRow、 和資料指標定位方法 (包括[moveToCurrentRow](../../connect/jdbc/reference/movetocurrentrow-method-sqlserverresultset.md)) 的結果集上呼叫。 MoveToInsertRow 方法會將結果集入插入模式中，有效地放和資料指標定位方法會中止插入模式。 相對的資料指標定位呼叫會移動游標相對於呼叫 moveToInsertRow 之前位於位置。 資料指標定位呼叫後，最終的目的地資料指標位置會變成新的資料指標位置。  
  
 如果資料指標定位呼叫在插入模式不成功時進行，稱為資料指標位置後失敗的呼叫前 moveToInsetRow 的原始資料指標位置。 如果 insertRow 失敗，資料指標仍然會在插入資料列上的資料指標仍然會在插入模式。  
  
 插入資料列中的資料行一開始會處於未初始化的狀態。 呼叫更新\<類型 > 方法將資料行狀態設定為初始化。 Get 呼叫\<類型 > 未初始化的資料行的方法會擲回的例外狀況。 InsertRow 方法的呼叫會傳回所有資料行插入資料列中以未初始化的狀態。  
  
 如果呼叫 insertRow 方法時，未初始化任何資料行，則會插入資料行的預設值。 如果沒有預設值，但是資料行允許為 NULL，則會插入 NULL。 如果沒有預設值，而且資料行不允許 NULL，則伺服器將會傳回錯誤，而且將會擲回例外狀況。  
  
> [!NOTE]  
>  GetRow 方法的呼叫會傳回 0，在插入模式時。  
>   
>  JDBC 驅動程式不支援定位更新或刪除。 根據 JDBC 規格， [setCursorName](../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)方法沒有任何作用， [getCursorName](../../connect/jdbc/reference/getcursorname-method-sqlserverresultset.md)方法會擲回例外狀況，如果呼叫。  
>   
>  唯讀和靜態資料指標絕對是不可更新的。  
>   
>  SQL Server 會將伺服器資料指標限制為單一結果集。 如果某個批次或預存程序包含多個陳述式，則必須使用順向唯讀用戶端資料指標。  
  
## <a name="see-also"></a>另請參閱  
 [使用 JDBC Driver 管理結果集](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  
