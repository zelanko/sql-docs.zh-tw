---
title: 註解 HelloData |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- hellodata sample application [ADO]
ms.assetid: a2831d77-7040-4b73-bbae-fe0bf78107ed
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d04b6f886a1f1a4583830d1afdd096b445461232
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="comments-on-hellodata"></a>HelloData 的註解
HelloData 應用程式逐步執行一般的 ADO 應用程式的基本作業： 取得、 檢視、 編輯和更新的資料。 當您啟動應用程式時，按一下第一個 按鈕，**取得資料**。 這樣將會執行**GetData**副程式。  
  
## <a name="getdata"></a>GetData  
 **GetData**將有效的連接字串放入一個模組層級變數， *m_sConnStr*。 如需連接字串的詳細資訊，請參閱[建立的連接字串](../../../ado/guide/data/creating-a-connection-string.md)。  
  
 指定錯誤處理常式使用 Visual Basic **OnError**陳述式。 如需在 ADO 中的錯誤處理的詳細資訊，請參閱[錯誤處理](../../../ado/guide/data/error-handling.md)。 新**連接**時會建立物件，而**CursorLocation**屬性設定為**adUseClient**因為 HelloData 範例會建立*中斷連接資料錄集*。 這表示，只要從資料來源擷取資料，與資料來源的實體連接已中斷，但您還是可以使用在本機快取的資料您**資料錄集**物件。  
  
 在開啟連接之後，請將 SQL 字串指派給變數 (sSQL)。 然後建立新的執行個體**資料錄集**物件`m_oRecordset1`。 在下一行程式碼中，開啟**資料錄集**透過現有**連接**，並傳入`sSQL`做為來源的**資料錄集**。 您協助 ADO 進行判斷，SQL 字串傳遞做為來源**資料錄集**是藉由傳遞命令的文字定義**adCmdText** 的最後一個引數中**資料錄集開啟**方法。 這一行也會設定**LockType**和**CursorType**聯**資料錄集**。  
  
 下的一行程式碼集**MarshalOptions**屬性等於**adMarshalModifiedOnly**。 **MarshalOptions**指出哪一筆記錄應該封送處理至中介層 （或 Web 伺服器）。 如需有關如何封送處理的詳細資訊，請參閱 COM 文件。 當您使用**adMarshalModifiedOnly**與用戶端資料指標 ([CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) = **adUseClient**)，在修改過的記錄用戶端被寫回中介層。 設定**MarshalOptions**至**adMarshalModifiedOnly**可以改善效能，因為較少的資料列會封送處理。  
  
 接下來，中斷**資料錄集**藉由設定其**ActiveConnection**屬性等於**Nothing**。 如需詳細資訊，請參閱 「 中斷連線和重新連線資料錄集 」 一節中[正在更新及保存資料](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
 關閉資料來源的連接並摧毀現有**連接**物件。 這會釋放它所耗用的資源。  
  
 最後一個步驟是設定**資料錄集**為**DataSource**針對 Microsoft DataGrid 控制項在表單上，您可以輕易顯示從資料**資料錄集**上表單。  
  
 按一下第二個按鈕，**檢查資料**。 這會執行**ExamineData**副程式。  
  
## <a name="examinedata"></a>ExamineData  
 ExamineData 使用各種方法和屬性的**資料錄集**物件，以顯示資料的相關資訊**資料錄集**。 它會使用報告的記錄數目**RecordCount**屬性。 執行迴圈**資料錄集**列印的值和**AbsolutePosition**屬性在表單上的 [顯示] 文字方塊中。 也在迴圈的值**書籤**第三筆記錄的屬性會被放入變數的變數， *vBookmark*，供日後使用。  
  
 此常式直接向後巡覽至使用先前儲存的書籤變數的第三個記錄。 此常式會呼叫**WalkFields**循環的副程式**欄位**集合**資料錄集**並顯示有關每個詳細資料**欄位**集合中。  
  
 最後， **ExamineData**使用**篩選**屬性**資料錄集**與這些記錄的螢幕**CategoryId**等於2。 套用此篩選條件的結果會立即顯示在方格中顯示表單上。  
  
 如需有關所示的功能**ExamineData**副程式，請參閱[檢查資料](../../../ado/guide/data/examining-data.md)。  
  
 接下來，按一下 第三個按鈕，**編輯資料**。 這樣將會執行**EditData**副程式。  
  
## <a name="editdata"></a>EditData  
 當程式碼進入**EditData**副程式，**資料錄集**仍篩選**CategoryId**等於 2，如此只有符合篩選條件的項目才會可見的。 第一次循環**資料錄集**並增加中每個可見項目的價格**資料錄集**百分之 10。 值**價格**欄位變更時，藉由設定**值**等於新的且有效的金額該欄位的屬性。  
  
 請記住，**資料錄集**中斷連接資料來源。 中所做的變更**EditData**只對在本機快取資料副本。 如需詳細資訊，請參閱[編輯資料](../../../ado/guide/data/editing-data.md)。  
  
 所做的變更不會建立資料來源上按一下第四個按鈕，直到**更新資料**。 這樣將會執行**UpdateData**副程式。  
  
## <a name="updatedata"></a>UpdateData  
 UpdateData 先移除篩選條件已套用至**資料錄集**。 程式碼會移除和重設`m_oRecordset1`為**DataSource** Microsoft 繫結 datagrid 在表單上，讓未篩選**資料錄集**出現在資料格中。  
  
 然後，程式碼會檢查以查看是否可以移動向後**資料錄集**使用**支援**方法**adMovePrevious**引數。  
  
 此常式會移至第一個記錄使用**MoveFirst**方法，並顯示欄位的原始值和目前值，使用**OriginalValue**和**值**屬性的**欄位**物件。 這些屬性搭配**UnderlyingValue**屬性 （未使用此處） 中討論[正在更新及保存資料](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
 下一步]、 [新**連接**物件建立，而且用來重新建立資料來源的連接。 您重新連線**資料錄集**藉由設定新的資料來源**連接**為**ActiveConnection**如**資料錄集**。 若要將更新傳送至伺服器，程式碼會呼叫**UpdateBatch**上**資料錄集**。  
  
 如果批次更新成功，模組層級旗標變數`m_flgPriceUpdated`，設定為 True。 這會提醒您更新版本，才能清除所有對資料庫所做的變更。  
  
 最後，程式碼移回至第一筆記錄**資料錄集**，並顯示原始和目前值。 值是相同的呼叫後方**UpdateBatch**。  
  
 如需如何更新資料的詳細資訊，包括要執行的工作時資料時的伺服器變更您**資料錄集**是中斷連接，請參閱[正在更新及保存資料](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
## <a name="formunload"></a>Form_Unload  
 **Form_Unload**副程式十分重要的原因。 首先，因為這是範例應用程式，Form_Unload 就會清除資料庫應用程式結束前所做的變更。 第二，程式碼會示範如何執行命令，直接從開啟**連接**物件使用**Execute**方法。 最後，它會顯示執行傳回非資料列 – 查詢 （更新） 對資料來源的範例。
