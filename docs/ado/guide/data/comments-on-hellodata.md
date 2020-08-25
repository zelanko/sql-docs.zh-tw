---
description: HelloData 的註解
title: HelloData 上的批註 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0593c95944c7109acb1d30f675a2375a5e20a668
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806331"
---
# <a name="comments-on-hellodata"></a>HelloData 的註解
HelloData 應用程式會逐步解說一般 ADO 應用程式的基本作業：取得、檢查、編輯和更新資料。 當您啟動應用程式時，按一下第一個按鈕， **取得資料**。 這將會執行 **[未** 執行] 的副程式。  
  
## <a name="getdata"></a>GetData  
 將有效的連接**字串放入**模組層級變數中， *m_sConnStr*。 如需連接字串的詳細資訊，請參閱 [建立連接字串](./creating-a-connection-string.md)。  
  
 使用 Visual Basic **OnError** 語句指派錯誤處理常式。 如需有關 ADO 中錯誤處理的詳細資訊，請參閱 [錯誤處理](./error-handling.md)。 建立新的 **連接** 物件，而且 **CursorLocation** 屬性設定為 **adUseClient** ，因為 HelloData 範例會建立已中斷連線的 *記錄集*。 這表示，只要從資料來源提取資料，與資料來源的實體連接就會中斷，但您仍然可以使用在 **記錄集** 物件中本機快取的資料。  
  
 開啟連接之後，將 SQL 字串指派給變數 (sSQL) 。 然後，建立新 **記錄集** 物件的實例 `m_oRecordset1` 。 在下一行程式碼中，透過現有的**連接**開啟**記錄**集，並傳入 `sSQL` 做為**記錄集**的來源。 您可以透過將最終引數中的**adCmdText**傳遞至**記錄集開啟**方法，協助 ADO 判斷您已傳遞做為**記錄集**來源的 SQL 字串是命令的文字定義。 這一行也會設定與**記錄集**相關聯的**LockType**和**CursorType** 。  
  
 下一行程式碼會將 **MarshalOptions** 屬性設定為等於 **adMarshalModifiedOnly**。 **MarshalOptions** 指出哪些記錄應該封送處理到仲介層 (或 Web 服務器) 。 如需封送處理的詳細資訊，請參閱 COM 檔集。 當您使用**adMarshalModifiedOnly**搭配用戶端資料指標時 ([CursorLocation](../../reference/ado-api/cursorlocation-property-ado.md)  =  **adUseClient**) ，只會將用戶端上修改過的記錄回寫到仲介層。 將 **MarshalOptions** 設定為 **adMarshalModifiedOnly** 可以改善效能，因為封送處理的資料列較少。  
  
 接下來，將 **記錄集** 的 **ActiveConnection** 屬性設為等於 **Nothing**，以中斷記錄集的連接。 如需詳細資訊，請參閱 [更新和保存資料](./updating-and-persisting-data.md)中的「中斷和重新連接記錄集」一節。  
  
 關閉與資料來源的連接，並終結現有的 **連接** 物件。 這會釋出所耗用的資源。  
  
 最後一個步驟是將 **記錄集** 設定為表單上 Microsoft DataGrid 控制項的資料 **源** ，如此您就可以輕鬆地在表單上顯示 **記錄集** 的資料。  
  
 按一下第二個按鈕， **檢查資料**。 這會執行 **ExamineData** 副程式。  
  
## <a name="examinedata"></a>ExamineData  
 ExamineData 會使用 **記錄集** 物件的各種方法和屬性，以顯示 **記錄集中**資料的相關資訊。 它會使用 **RecordCount** 屬性來報告記錄的數目。 它會迴圈查看 **記錄集** ，並在表單上的 [顯示] 文字方塊中列印 **AbsolutePosition** 屬性的值。 此外，在迴圈中，第三筆記錄的 [ **書簽** ] 屬性值會放入 Variant 變數 *vBookmark*中，以供稍後使用。  
  
 常式會使用先前儲存的書簽變數，直接流覽回第三筆記錄。 常式會呼叫**WalkFields**副程式，這會在**記錄集**的**Fields**集合中迴圈，並顯示集合中每個**欄位**的詳細資料。  
  
 最後， **ExamineData**只會針對**具有等於 2**之欄位集的記錄，使用**記錄集**的**Filter**屬性來進行畫面。 套用此篩選的結果會立即顯示在表單上的顯示格線中。  
  
 如需 **ExamineData** 副程式中所顯示功能的詳細資訊，請參閱 [檢查資料](./examining-data.md)。  
  
 接著，按一下第三個按鈕， **編輯資料**。 這會執行 **EditData** 副程式。  
  
## <a name="editdata"></a>EditData  
 當程式碼進入 **EditData** 副程式時，仍會將 **記錄集** 的篩選器篩選 **為等於 2** ，因此只會顯示符合篩選準則的專案。 它會先迴圈查看 **記錄集** ，並將 **記錄集中** 每個可見專案的價格增加10%。 將該欄位的 [**值**] 屬性設定為等於新的有效數量，即可變更 [ **Price** ] 欄位的值。  
  
 請記住， **記錄集會** 與資料來源中斷連接。 在 **EditData** 中所做的變更只會對本機快取的資料複本進行。 如需詳細資訊，請參閱 [編輯資料](./editing-data.md)。  
  
 在您按一下第四個按鈕、 **更新資料**之前，將不會在資料來源上進行變更。 這會執行 **UpdateData** 副程式。  
  
## <a name="updatedata"></a>UpdateData  
 UpdateData 會先移除已套用至 **記錄集**的篩選。 程式碼會移除並重設 `m_oRecordset1` 為表單上 Microsoft 系結 DataGrid 的 **DataSource** ，讓未篩選的 **記錄集** 出現在方格中。  
  
 然後，程式碼會使用**支援**方法搭配**adMovePrevious**引數，以查看您是否可以在**記錄集中**向前移動。  
  
 常式會使用**MoveFirst**方法移至第一筆記錄，並使用**Field**物件的**OriginalValue**和**Value**屬性來顯示該欄位的原始值和目前值。 [更新和保存資料](./updating-and-persisting-data.md)時，這些屬性與**UnderlyingValue**屬性 (不會在) 中使用）會進行討論。  
  
 接下來，會建立新的 **連接** 物件，並使用它來重新建立與資料來源的連接。 您可以藉由將新**連接**設定為**記錄集**的**ActiveConnection** ，將**記錄集**重新連接到資料來源。 為了將更新傳送至伺服器，程式碼會呼叫**記錄集**上的**UpdateBatch** 。  
  
 如果批次更新成功，模組層級旗標變數 `m_flgPriceUpdated` 就會設定為 True。 這會提醒您稍後清除對資料庫所做的所有變更。  
  
 最後，程式碼會移回 **記錄集** 內的第一筆記錄，並顯示原始和目前的值。 呼叫 **UpdateBatch**之後，值會相同。  
  
 如需有關如何更新資料的詳細資訊，包括當您的 **記錄集** 中斷連接時，伺服器上的資料發生變更時該怎麼做，請參閱 [更新和保存資料](./updating-and-persisting-data.md)。  
  
## <a name="form_unload"></a>Form_Unload  
 **Form_Unload**副程式很重要，原因有很多。 首先，因為這是範例應用程式，Form_Unload 會在應用程式結束之前清除對資料庫所做的變更。 其次，此程式碼會示範如何使用**Execute**方法，從開啟的**連接**物件直接執行命令。 最後，它會顯示執行非資料列傳回查詢的範例， (針對資料來源) 的更新查詢。