---
title: HelloData 的註解 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hellodata sample application [ADO]
ms.assetid: a2831d77-7040-4b73-bbae-fe0bf78107ed
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3086eff0e4a774e7f63e7ff876a9675668d5912
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47707876"
---
# <a name="comments-on-hellodata"></a>HelloData 的註解
HelloData 應用程式會逐步引導一般的 ADO 應用程式的基本作業： 取得、 檢查、 編輯和更新資料。 當您啟動應用程式時，按一下第一個按鈕中，**取得資料**。 這會執行**GetData**副程式。  
  
## <a name="getdata"></a>GetData  
 **GetData**將有效的連接字串放入一個模組層級變數， *m_sConnStr*。 如需有關連接字串的詳細資訊，請參閱 <<c0> [ 建立的連接字串](../../../ado/guide/data/creating-a-connection-string.md)。  
  
 將指定的錯誤處理常式，使用 Visual Basic **OnError**陳述式。 如需有關在 ADO 中的錯誤處理的詳細資訊，請參閱[錯誤處理](../../../ado/guide/data/error-handling.md)。 新**連接**會建立物件，而**CursorLocation**屬性設定為**adUseClient**因為 HelloData 範例會建立*中斷連接資料錄集*。 這表示，只要從資料來源擷取資料，與資料來源的實體連接已中斷，但您仍然可以使用在本機快取資料您**資料錄集**物件。  
  
 在開啟連接之後，請將 SQL 字串指派給變數 (sSQL)。 然後建立新的執行個體**Recordset**物件， `m_oRecordset1`。 在下一行程式碼中，開啟**資料錄集**現有**連線**，並傳入`sSQL`做為來源**資料錄集**。 您有助於 ADO 讓 SQL 字串，判斷做為來源已通過**資料錄集**是藉由傳遞的命令的文字定義**adCmdText** 的最後一個引數中**資料錄集開放**方法。 這一行也會設定**LockType**並**CursorType**相關聯**資料錄集**。  
  
 程式碼集的下一行**MarshalOptions**屬性等於**adMarshalModifiedOnly**。 **MarshalOptions**指出哪些記錄應該封送處理至中介層 （或 Web 伺服器）。 如需有關如何封送處理的詳細資訊，請參閱 COM 文件。 當您使用**adMarshalModifiedOnly**與用戶端資料指標 ([CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) = **adUseClient**)，在修改過的記錄用戶端會回寫至中介層。 設定**MarshalOptions**要**adMarshalModifiedOnly**可以改善效能，因為較少的資料列封送處理。  
  
 接下來，中斷**Recordset**藉由設定其**ActiveConnection**屬性等於**Nothing**。 如需詳細資訊，請參閱 「 中斷連線並重新連接資料錄集 」 一節中[更新和保存資料](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
 關閉資料來源的連接，然後終結現有**連線**物件。 這會釋放它所使用的資源。  
  
 最後一個步驟是設定**Recordset**做為**DataSource** Microsoft DataGrid 控制項在表單上因此，您可以輕鬆地顯示從資料**資料錄集**上表單。  
  
 按一下第二個按鈕中，**檢查資料**。 這會執行**ExamineData**副程式。  
  
## <a name="examinedata"></a>ExamineData  
 各種方法和屬性，會使用 ExamineData**資料錄集**來顯示資料的相關資訊的物件**資料錄集**。 它會使用報告的記錄數目**RecordCount**屬性。 會循環**Recordset** ，並列印的值**AbsolutePosition**在表單上的 [顯示] 文字方塊中的屬性。 在迴圈中，值也同時**書籤**第三個記錄的屬性會放入變數的變數， *vBookmark*，以供稍後使用。  
  
 常式直接向後巡覽至使用先前儲存的書籤變數的第三個記錄。 此常式會呼叫**WalkFields**循環的副程式**欄位**的集合**資料錄集**，並顯示詳細說明每一個**欄位**集合中。  
  
 最後， **ExamineData**會使用**篩選**屬性**資料錄集**只有這些記錄的畫面**CategoryId**等於2。 套用此篩選條件的結果會立即顯示在表單上的顯示格線項目。  
  
 如需有關所示的功能**ExamineData**副程式，請參閱[檢查資料](../../../ado/guide/data/examining-data.md)。  
  
 接下來，按一下 第三個按鈕中，**編輯資料**。 這會執行**EditData**副程式。  
  
## <a name="editdata"></a>EditData  
 當程式碼進入**EditData**副程式**資料錄集**仍然篩選**CategoryId**等於 2，如此只有符合篩選準則的項目才會可見的。 第一次循環**Recordset** ，並增加每個可見的項目中的價格**資料錄集**百分之 10。 值**價格**欄位已變更設定**值**新的且有效的量等於該欄位的屬性。  
  
 請記住**資料錄集**已中斷連接資料來源。 中所做的變更**EditData**只對資料的本機快取副本。 如需詳細資訊，請參閱 <<c0> [ 編輯資料](../../../ado/guide/data/editing-data.md)。  
  
 所做的變更將不在資料來源上進行，直到您按一下第四個按鈕，**更新資料**。 這會執行**UpdateData**副程式。  
  
## <a name="updatedata"></a>UpdateData  
 UpdateData 先移除已套用的篩選條件**資料錄集**。 程式碼會移除和重設`m_oRecordset1`做為**DataSource**表單上的 Microsoft 繫結 DataGrid 的以便未篩選**資料錄集**出現在資料格中。  
  
 然後，程式碼會檢查以查看您是否可以將移向後**資料錄集**利用**支援**方法**adMovePrevious**引數。  
  
 常式會將移至第一個記錄使用**MoveFirst**方法，並顯示欄位的原始和目前值，藉由使用**OriginalValue**並**值**屬性**欄位**物件。 這些屬性連同**UnderlyingValue**屬性 （未使用此），會討論[正在更新及保存資料](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
 接下來，新**連線**物件是建立，用來重新建立資料來源的連接。 您重新連接**資料錄集**藉由設定新的資料來源**連線**作為**ActiveConnection**如**資料錄集**。 若要將更新傳送到伺服器，也就是程式碼會呼叫**UpdateBatch**上**資料錄集**。  
  
 如果批次更新成功，模組層級旗標變數`m_flgPriceUpdated`，設定為 True。 這會提醒您更新版本，以清除所有對資料庫所做的變更。  
  
 最後，程式碼會將移回中的第一個資料錄**資料錄集**並顯示原始值和目前值。 值則會在呼叫之後是相同**UpdateBatch**。  
  
 如需如何更新資料的詳細資訊，包括時該怎麼做資料時的伺服器變更您**資料錄集**是中斷連接，請參閱[正在更新及保存資料](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
## <a name="formunload"></a>Form_Unload  
 **Form_Unload**副程式十分重要的幾個原因。 首先，因為這是一個範例應用程式，Form_Unload 就會清除資料庫應用程式結束前所做的變更。 第二，程式碼會示範如何執行命令，直接從開放**連接**使用的物件**Execute**方法。 最後，它會顯示執行不傳回資料列 – 查詢 （更新） 對資料來源的範例。
